Step Project 2
Task
Create a test [GitHub repository](https://github.com/Visemir/step2) with a Node.js app from forStep2. 

Create a test account in Docker Hub (free): Docker Hub

Using [Vagrant](https://github.com/Visemir/danitProjekt02/blob/master/Vagrantfile), create two VMs: one for the Jenkins server and the second for the Jenkins worker.

Manually or in the Vagrant file, add installation of Docker and Docker Compose on the first VM.
Manually or using the Vagrant file, add installation of Docker and Jenkins worker directly on the second VM (without Docker).
Connect the Jenkins worker to the master node. Check that you can run a test pipeline on the Jenkins worker.

![](https://github.com/Visemir/danitProjekt02/blob/master/jenkistes2.jpg)

Add credentials with your Docker Hub username and password to Jenkins credentials.

![](https://github.com/Visemir/danitProjekt02/blob/master/creddok.jpg)

Create a [test pipeline](https://github.com/Visemir/danitProjekt02/blob/master/TestPipeline2) using the Groovy language, which will start when you push to the repository from task 1. The pipeline must:

Pull the code.

![](https://github.com/Visemir/danitProjekt02/blob/master/step01.jpg)

Build the Docker image on the Jenkins worker.

1[](https://github.com/Visemir/danitProjekt02/blob/master/step02.jpg)

Run the Docker image with tests.

![](https://github.com/Visemir/danitProjekt02/blob/master/step03.jpg)
![](https://github.com/Visemir/danitProjekt02/blob/master/step04.jpg)


If the tests are successful, log in to your Docker Hub account using Jenkins credentials from step 7 and push the built image to Docker Hub.

![](https://github.com/Visemir/danitProjekt02/blob/master/steep05.jpg)

If the tests fail, print the message "Tests failed".

![](https://github.com/Visemir/danitProjekt02/blob/master/step06.jpg)
