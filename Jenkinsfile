#!/usr/bin/env groovy
//@Library('my-shared-library@master') _ //explicit call to sl
pipeline {

  agent {label 'ec2'}

  libraries {
  lib('my-shared-library@master')
  lib('jenkins_docker_lib@master')
  lib('jenkins_artifactory_lib@master')
  }

  options {
    disableConcurrentBuilds()
    timestamps()
  }

  stages {
    stage ('dockerbuild') {
      steps {
        dockerBuild()
      }
    }

    stage ("BuildArtifactory") {
      steps {
        artifactorybuilder('build','*.jar','')
      }
    }  

    stage ('check logs') {
      steps {
        filterLogs('Warning',1)
      }
    }
    
    stage ('docker push') {
      steps {
        dockerPush()
      }
    }
  }
}
