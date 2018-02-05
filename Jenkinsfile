node {
    stage('Preparation') {
        checkout scm
    }
    stage('Build') {
        withMaven(jdk: 'JDK8', maven: 'Maven 3.5.x', mavenSettingsConfig: 'maven-settings') {
            def branchName = env.BRANCH_NAME
            echo "Building branch ${branchName}..."

            if("master".equals(branchName)) {
                sh "mvn clean test sonar:sonar deploy -DdeployAtEnd=true"
            }

        }
    }
    stage('Results') {
        junit '**/target/surefire-reports/TEST-*.xml'
        archive '**/target/*.jar'
    }
}