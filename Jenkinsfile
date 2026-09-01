node {

    def mavenHome = tool name: 'Maven'

    stage('Git Checkout') {
        git branch: 'main',
            url: 'https://github.com/devOps-lasya/maven-webapplication-project.git'
    }

    stage('Compile') {
        sh "${mavenHome}/bin/mvn compile"
    }

    stage('Build Artifact') {
        sh "${mavenHome}/bin/mvn clean package"
    }

    stage('SQ Report') {
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }

    stage('Deploy Artifact') {
        sh "${mavenHome}/bin/mvn deploy"
    }

    stage('Deploy to Tomcat') {
        sh '''
            curl -v -u kk:password\
            --upload-file /var/lib/jenkins/workspace/scripted-way-pl-1/target/maven-web-application.war \
            "http://13.204.75.85:8080/manager/text/deploy?path=/maven-web-application&update=true"
        '''
    }
}

