node{
    stage('Git upload'){
        git credentialsId: 'demo', url: 'https://github.com/Prabhu4tx/addressbook'
        
    }
    stage('Maven build'){
        def MavenHome = tool name: 'maven', type: 'maven'
        def mvnCMD = "${MavenHome}/bin/mvn"
        sh "${mvnCMD} clean compile"
        sh "${mvnCMD} package"
        
    }
    stage ('docker build')
    {
      // sh  "docker version"
        sh " docker build -t cybersolvedocker/myapp2:2.1.22 ."
    }
    stage ('push docker image')
    {
        withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerpwd')]) {
            sh "docker login -u cybersolvedocker  -p ${dockerpwd}"
      
}
   sh 'docker push cybersolvedocker/myapp2:2.1.22'
    }
    stage ('Run tomcatapp'){
    sh 'docker run -p 8081:8081 -d --name myapp2 cybersolvedocker/myapp2:2.1.22'   
  }
}
