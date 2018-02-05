node {
    def mvnHome
    stage('Preparation') {
        git 'git@github.com:jwcarman/pcf-demo.git'
        mvnHome = tool 'Maven 3.5.x'
    }
    stage('Build') {
        withMaven(jdk: 'JDK8', maven: 'Maven 3.5.x', mavenSettingsConfig: 'maven-settings') {
            sh "mvn clean deploy"
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive '**/target/*.jar'
    }
}