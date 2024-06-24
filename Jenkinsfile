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
        SONARSCANNER = "sonarqubescanner"
        SONARSERVER = "sonarserver"
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
        stage('CODE ANALYSIS with SONARQUBE') {
          
		  environment {
            scannerHome = tool "${SONARSCANNER}"
          }

          steps {
            withSonarQubeEnv("${SONARSERVER}") {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
            }
          }
        }
        stage ("quality Gate check"){
            steps {
            timeout(time: 1, unit: 'HOURS') {
               waitForQualityGate abortPipeline: true
            }
        } 
    }
}
}