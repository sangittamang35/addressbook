node{
    stage('Git upload'){
        git credentialsId: 'github-key',  url: 'git@github.com:sangittamang35/addressbook.git'
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
        sh " docker build -t samtam/myapp2:2.1.22 ."
    }
    stage ('push docker image')
    {
        withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerpwd')]) {
            sh "docker login -u samtam -p ${dockerpwd}"
      
}
   sh 'docker push samtam/myapp2:2.1.22'
    }
    stage ('Run tomcatapp'){
    sh 'docker run -p 8181:8181 -d --name myapp2 samtam/myapp2:2.1.22'   
  }
}
