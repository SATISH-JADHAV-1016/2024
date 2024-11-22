pipeline{
        agent{
           label{
               label 'built-in'
               customWorkspace '/root/Container/'
                }
              }
    stages{
       
         stage('create container'){
             steps{
                sh "rm -rf"
                 sh "docker run -dp 80:80 --name container httpd"
                  }
                                  }
     
          stage('deploy'){
             steps{
                sh "docker cp index.html container:/usr/local/apache2/htdocs"
                sh "docker exec container chmod 755 /usr/local/apache2/htdocs/index.html"
                  }
                        }
           }
   }
