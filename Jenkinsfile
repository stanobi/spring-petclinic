
node {

   stage('Clone Repository') {
        // Get some code from a GitHub repository
        git 'https://github.com/stanobi/spring-petclinic.git'
    
   }
   stage('Build Maven Image') {
        docker.build("maven-build")
   }
   
   stage('Run Maven Container') {
       
        //Remove maven-build-container if it exisits
       shell " docker rm -f maven-build-container"
        
        //Run maven image
       shell "docker run --rm --name maven-build-container maven-build"
   }
   
   stage('Deploy Spring Boot Application') {
        
         //Remove maven-build-container if it exisits
       shell " docker rm -f java-deploy-container"

       shell "docker run --name java-deploy-container --volumes-from maven-build-container -d -p 9999:9999 denisdbell/petclinic-deploy"
   }

}
