#!/usr/bin/env groovy
//@Library('my-shared-library@master') _ //explicit call to sl
pipeline {
  agent {
    label 'ec2'
  }
  libraries {
  lib ('my-shared-library@master')
  lib('jenkins_global_lib@master')
}
options {
  timestamps()
}
  stages {
    stage ('Build') {
      steps {
        builder('build','trainSchedule.zip')
      }
    }
    stage ('check logs') {
      steps {
        filterLogs('Warning',1)
      }
    }
    stage ('dockerbuild') {
      steps {
        dockerBuild dockerfile:'./files/DockerFile'
        dockerbuild imageName: 'any_name'
    }
      }
    }
}
