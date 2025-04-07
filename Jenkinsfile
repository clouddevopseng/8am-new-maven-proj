node {
    stage('Download code from git source code management') {
    git branch: 'prod', url: 'https://github.com/clouddevopseng/8am-new-maven-proj.git'
     }
     stage('Covert artifacts into war formate') {
    sh 'mvn package'
     }
     stage('Deployment into a container') {
    deploy adapters: [tomcat9(credentialsId: 'prod', path: '', url: 'http://15.207.111.233:8080/')], contextPath: '/prod-7th', war: '**/*.war'}
}
