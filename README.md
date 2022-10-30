# todo-fe
* Pipeline (Jenkinsfile)-

   * This is a containerized pipeline which uses Dockerfile-pipeline to build the image, and contains the stages:  Build, Test, Delivery, Cleanup and Push (to Dockerhub).
  
        In order to run the pipeline which pushes the frontend image to your Dockerhub, you will need to add the credentials on your jenkins locally:

        Dashboard > Manage Jenkins > Credentials.
  
        Otherwise comment the environment and the 'Push' stage.
   
        Same is with todo-be (backend): https://github.com/RafGarn/todo-be
* After running both frontend and backend pipelines:
   * Now you can combine it all together and run on your local machine the commend: 
   
         docker-compose up -d .
     To see all the containers that are up now: 
     
         docker compose ps
         
      And now you can check if the todo application is up and running in your browser:
      
        
         http://localhost:3000
    * The docker-compose.yaml file contains the images you've created and pushed to the Dockerhub and also pulls the mongodb image.
     
  
 
