node {
    stage('Download code from git source code management') {
    git branch: 'test', url: 'https://github.com/clouddevopseng/8am-new-maven-proj.git'
     }
     stage('Covert artifacts into war formate') {
    sh 'mvn package'
     }
     stage('Deployment into a container') {
    deploy adapters: [tomcat9(credentialsId: 'test', path: '', url: 'http://43.204.98.191:8080/')], contextPath: '/test-7th', war: '**/*.war'
    }
}
