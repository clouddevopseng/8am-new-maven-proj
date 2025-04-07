node {
    stage('Download code from git source code management') {
    git branch: 'dev', url: 'https://github.com/clouddevopseng/8am-new-maven-proj.git'
     }
     stage('Covert artifacts into war formate') {
    sh 'mvn package'
     }
     stage('Deployment into a container') {
    deploy adapters: [tomcat9(credentialsId: '744b5888-d282-40a1-9a1d-1aa50b4df9e4', path: '', url: 'http://3.110.165.7:8080/')], contextPath: '/dev-7th', war: '**/*.war'
     }
}
