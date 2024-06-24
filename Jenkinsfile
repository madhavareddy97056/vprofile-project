pipeline {
    agent any
    tools {
        jdk "java8"
        maven "maven3"
    }
    environment {
        SNAP-REPO="vprofile-snapshot"
        NEXUS-USER="admin"
        NEXUS-PASS="admin123"
        RELEASE-REPO="vprofile-release"
        CENTRAL-REPO="vpro-maven-central"
        NEXUS-GRP-REPO="vpro-maven-group"
        NEXUSIP="http://65.0.181.113/"
        NEXUSPORT="8081"
        NEXUS-LOGIN="nexuslogin"
    }
    stages {
       stage ("build"){
        steps {
            sh "mvn -s settings.xml -DskipTests install"
        }
       }
    }
}