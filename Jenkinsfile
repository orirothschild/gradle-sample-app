#!/usr/bin/env groovy
//@Library('my-shared-library@master') _ //explicit call to sl
pipeline {
agent {label 'ec2'}
libraries {
lib ('my-shared-library@master')
lib('jenkins_global_lib@master')
}
options {timestamps()}
  stages {
      // stage ('Build') {
      //   steps {
      //     builder('build','trainSchedule.zip')
      //   }
      // }
    stage ('dockerbuild') {
      steps {
        dockerBuild()
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
