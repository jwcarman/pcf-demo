node {
    def mvnHome
    stage('Preparation') {
        git 'git@github.com:jwcarman/pcf-demo.git'
        mvnHome = tool 'Maven 3.5.x'
    }
    stage('Build') {
        sh "'${mvnHome}/bin/mvn' clean deploy"
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive '**/target/*.jar'
    }
}