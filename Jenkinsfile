node {
    def mvnHome
    stage('Preparation') {
        git 'git@github.com:jwcarman/pcf-demo.git'
        mvnHome = tool 'Maven 3.5.x'
    }
    stage('Build') {
        // Run the maven build
        if (isUnix()) {
            sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
        } else {
            bat(/"${mvnHome}\bin\mvn" -Dmaven.test.failure.ignore clean package/)
        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive 'target/*.jar'
    }
    stage('PWS') {
        pushToCloudFoundry cloudSpace: 'development', credentialsId: 'pcf', manifestChoice: [manifestFile: 'target/classes/manifest.yml'], organization: 'microbule', target: 'https://api.run.pivotal.io'
    }
}