# MLOps Task-3


Task description

1.	Create container image that’s has Python3 and Keras or numpy  installed  using dockerfile 

2.	When we launch this image, it should automatically starts train the model in the container.

3.	Create a job chain of job1, job2, job3, job4 and job5 using build pipeline plugin in Jenkins 

4.	 Job1 : Pull  the Github repo automatically when some developers push repo to Github.

5.	 Job2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).

6.	Job3 : Train your model and predict accuracy or metrics.

7.	Job4 : if metrics accuracy is less than 80%  , then tweak the machine learning model architecture.

8.	Job5: Retrain the model or notify that the best model is being created

9.	Create One extra job job6 for monitor : If container where app is running. fails due to any reason then this job should automatically start the container again from where the last trained model left

Tools used to Create-
Github- for hosting our  repositoy.
Jenkins-isuse to automate various jobs.
Redhat8-use as a base OS for running the services like httpd,ngrok,jenkins.
Docker- to run containner image in python model.

Creating a dockerfile :

In RHEL8 fisrt make a directory that will store all the data or the program for our machine learning model.

    mkdir Code

Now the jenkins will automatically copy the files in this folder.
Download a centos:7 image in docker using:

docker pull centos:7
docker run -it --name os centos:7

Now install al the requirements for the Machine learning model.
After the requirements are fulfilled use commit command to make your own image and we will use this image in our Dockerfile.

  docker commit os myimage:v2

Now type:

 vim Dockerfile

And write the following code:

FROM: myimage:v2
RUN mkdir /root/my_model
VOLUME /root/my_model
COPY ./Code/. ./root/my_model/
WORKDIR /root/my_model
CMD ["python3","code_file2.py"]

Save this docker file and now build two different images for different environments:

 docker build -t deep:v1 /root
 docker build -t neural_net:v1 /root

Create job1
Job1 : Pull  the Github repo automatically when some developers push repo to Github.
job1 Congiguration

Creating Job2
By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).
