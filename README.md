# todo-fe
* Pipeline-

  In order to run the pipeline which pushes the frontend image to Dockerhub, you will need to add the credentials on your jenkins locally:

  Dashboard > Manage Jenkins > Credentials.
   Otherwise comment the environment and the 'Push' stage.
  
 * This is a containerized pipeline which uses Dockerfile-pipeline to build the image.
