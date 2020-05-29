# MLOps Task-3

What is MLOps?
ML and DevOps when together used forms a powerful combination which is called MLOps.

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

Create job1-
 Job1 : Pull the Github repo automatically when some developers push repo to Github. job1 Congiguration.

1)Enter a Job Name, select “Freestyle project” and hit “OK” button.

2)Source Code Management: The section contents the source code options select GIT.

3)Build Triggers: The section contents trigger settings that trigger the build based on the specific condition match.

4)Build: The section contents the build steps that can be performed by adding Batch or shell command.

5) Post-build Actions: The section contents the build steps that can be performed after the build action done.
By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code  and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).
Creating job 2-
Job2 : By looking at the code or program file, Jenkins should automatically start the respective machine learning software installed interpreter install image container to deploy code and start training( eg. If code uses CNN, then Jenkins should start the container that has already installed all the softwares required for the cnn processing).Run docker container from docker image-

Configure Email notification in jenkins :

Click the ‘Manage Jenkins’ menu option displayed at the right side of the screen. You will be redirected to the ‘Manage Jenkins’ page, where you need to select the ‘Manage Plugin’ option.

Click the ‘Available’ tab then Manage Plugin page.

Start typing ‘Notification’ in the ‘Filter’ as ‘Manage Plugin’ page. Click the checkbox next to the ‘Email-ext plugin’ option. Click the ‘Install without restart’ button.

Now, click the checkbox next to the ‘Email-ext Template Plugin’ option. Click the ‘Install without restart’ button.

Go to the Jenkins home page and click the ‘Manage Jenkins’ menu option. Then, select the ‘Configure System’ option.

Enter the SMTP server name under ‘Email Notification’. Click the ‘Advanced’ button and then click the checkbox next to the ‘Use SMTP Authentication’ option. Now, set the following fields.

SMTP server name : smtp.gmail.com
User name: user_email_id@gmail.com
Password: abcd
Use SSL : Checked
SMTP Port: 456


Creating Job3 in jenkins
JOB3 has a task to copy the [show_output.html] file from Parent Directory to /var/www/html which is the default directory for webpages in Apache Webserver.


Creating Job 4-
Job4 : Train your model and predict accuracy or metrics.
if metrics accuracy is less than 80% , then tweak the machine learning model architecture.

Creating JOB5 in Jenkins-
After getting the desired accuracy it will run. This job will run model_success_mail.py and send the notification of project completion to developer.

For more content refer to my blog on Linkedin.
Thank you for reading.
