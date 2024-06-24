pipeline {
    agent any
    tools {
        jdk "java8"
        maven "maven3"
    }
    environment {
        SNAP_REPO = "vprofile-snapshot"
        NEXUS_USER = "admin"
        NEXUS_PASS = "admin123"
        RELEASE_REPO = "vprofile-release"
        CENTRAL_REPO = "vpro-maven-central"
        NEXUS_GRP_REPO = "vpro-maven-group"
        NEXUSIP = "65.0.181.113"
        NEXUSPORT = "8081"
        NEXUS_LOGIN = "nexus_creds"
    }
    stages {
       stage ("build"){
        steps {
            sh "mvn -s settings.xml -DskipTests install"
        }
        post {
            success {
                echo 'archiving artifact'
              archiveArtifacts artifacts: "**/*.war"
            } 
        }
       }
       stage ("test"){
        steps {
            sh "mvn -s settings.xml test"
        }
       }
       stage ("checkstyle analysis"){
        steps {
            sh "mvn -s settings.xml checkstyle:checkstyle"
        }
       }
    }
}