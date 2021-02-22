podTemplate(label: 'mypod', containers: [
  containerTemplate(name: 'git', image:w 'alpine/git', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'maven', image: 'maven:3.3.9-jdk-8-alpine', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true)
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ] 
  ) {
     node{
    	stage('SCM Checkout')
        {
        git credentialsId: '4cc785e9-441d-4818-a248-2bfb2148004d', url: 'https://github.com/VardhanNS/phpmysql-app.git'
        }
    
        stage('Run Docker Compose File')
        {
           container('docker'){
           sh 'docker-compose build'
           sh 'docker-compose up -d'
           }
        }

        stage('PUSH image to Docker Hub')
        {
        container('docker'){     
             sh 'sudo docker login -u "pkamalsai" -p "k@malkee3014" docker.io'
             //sh 'sudo docker push upasanatestdocker/mysql'
             //sh 'sudo docker push upasanatestdocker/job1_web1.0'
             sh 'sudo docker push pkamlsai/job1_web2.0'
            // sh 'docker push upasanatestdocker/mysql'
             }
         }
      }
}
