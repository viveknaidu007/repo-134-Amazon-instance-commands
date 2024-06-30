# repo-134-Amazon-instance-commands
here im giving the notes for deployinf the instances , so that i can refere her eany time




# How to deploy in ec2 instance?

"https://www.youtube.com/watch?v=kQ9qiIzsFxM&t=1s"

# What is ec2 instance?

go to aws
click EC2

Remember we are deploying the entire ml project in ec2 instance

1. Click EC2
2. Click Instances
3. Launch New Instances
   (i)  give names and tags
  (ii) choose machine (amazon linux machine)
 (iii) choose ami (amazon machine image) and bit (by default)
4. choose instance type (t2.micro free tier)
5. key pair login (it is nothing but, in order to use the particular instance we need that key pair)
    give the key pair name & download the .pem file

6. just click launch instance
7. go to ec2 and click instance, there our instance has been created

I have started my instance, basically, I have created a server in somewhere in the cloud,
In that particular cloud, I have a linux software system, I have a cpu, I have some information over there, I have a resources, I have some harddisk over there.

What I want to do this now is,
I have take my entire code and put it over there


next step.


now, how to be deploy that code in that linux server? 

we have connecting to the vm (virtual machine)
but how can we connect?

 basically there is a putty, now we have to use putty.

just download the putty generator for windows and winscp

8. open putty gen

putty key generator

why putty key generator?

	convert from .pem to .ppk
	it will create a .ppk file
	.ppk file full form is nothing but, it is a public private key pair.

9. click load in putty key generator
10. select that downloaded pem file
	then we will get a successfully imported box

11. now we need to save it, how?
save it in a private key.

save in the directory, with same file name of .pem file
(here our pem file name is testrevenue.pem)
so I saved in the name of testrevenue.ppk

now file was saved

then close the putty gen

now go back to putty

12. open putty

this putty will actually help me to connect to the ec2 instance.

ok now we have to connect to the ec2 instance

	(i) host name - where we find?
			go back to aws instance, just scroll to the right hand side, there you can find the public ipv4, just copy it. and paste it over here.
	(ii) then now, we have to named that session, in saved sessions box, just give the name, testrevenue

	(iii) in next thing we have to do, go in connection and select data, inside this data, there is asking for auto login username

	where do i get this login username?

	go to aws, and select that instance, and click connect, inside the connect go to ec2 instance connect, there we can able to find out the username, here our user name is ubuntu.(by default),
	so here, in putty, I am also going to write default name.
	in my aws, i have a default name that is ec2-user, so here I am going to write the ec2-user.

next step

	(iv) go to SSH, & click auth,
	inside this auth, there is asking for the private key file for authentication.

	where I can it? 

	we downloaded .ppk file before,
	whereever I downloaded the .ppk file, i have to put over here. so that it will be able to login or use that particular instance.

	click browse and select that converted ppk file.

	(v) now go back to session in putty gen.
	click putty gen. in saved session box, i just written a test_revenue, i just go and save it.

so that i will not lose that particular data, suppose if get disconnected to that particular data, then again I have to fillup all these informations, so now save it the saved session name.

	(vi) now select that saved session name, (test_revenue)

	select test_revenue and click open

then we will get a warning box, just click yes, 

now one new cmd will open, that is nothing but, it is our ubuntu terminal prompt.

now I am inside that ec2 instance, which is there in the cloud.

this is the bash terminal.

now, just do pip install pandas, 
it is showing pip command not found

then i check python3, it is available,
then i clear the screen using clear command

now the next thing is that, 

13. I have to push all the entire files (entire project files and folders) files to my ec2 instance.

how do we push it?

in order to do, there is a another tool, that is winscp.

here winscp comes into the picture. (we can use filezilla as well.)

14. now go to app.py file,

	inside that, we have to make some changes.
that is he used one 1 deep learning result in that project out of 3. so he just comment it, because in cloud there is a 1gb of ram, so he just commented that deep learning project code inside the app.py

	inside the app.run we have return debug=True,
instead of that, we need to change that to host=0.0.0.0, and port=8080

why we need to change it?
why specifically 0.0.0.0 and 8080, because by default, if you are try to use some http protocol or all the traffic protocal in aws instance, it wil taking the by default port as 8080 and  and it will be taking the default ip as 0.0.0.0, so instead of writing app.run(debug=True),
write like this

15. after downlaoding the winscp just install it.
now open winscp

	(i) it will asking again the host name,
	where can I find this?
	go to ec2 instance, there public ip address is available, just copy it and paste it over here. in new site (inside the host name paste it)

	(ii) then give the username, that is bydefault name give it. (for krish it is ubuntu, for me it is ec2-user)

	(iii) Then click advance

	(iv) there in SSH ----> Authentication, we have to put our ppk file here also.

	(v) then click ok

	(vi) then click login

	(vii) then one new box will come, just select yes (accept)

	(viii) then one new box will come, in lhs what file we have in our system, in rhs what file having in cloud (ubuntu server)
	there is nothing file, so we have to select it and move it over here.
	open the ubuntu terminal prompt and check it (using ls command)

	(ix) in lhs, the entire project files and folder is there, 

now what I am going to do is that, what part of the file i need to deploy it over here, 
so just drag & drop the required files & folders only,

he have a procfile in local & but he dont need that in ubutu (cloud), because procfile is for heroku platform.

now go back to putty, & type ls
you can able to see the all files and folders over here.



just drag & drop the important files.
	
16. just clear the ubuntu screen, using clear command

17. the first thing inside your ubuntu server in instance type, you have to basically do is that pip3 install -r requirements.txt and just enter it

	he made some changes in his requirements.txt, because he have pytorch library.  so he comment it. he used openwith notepad++ and changed(after changed that changes, he just again moved that)

18. Error showing, that is pip3 not command found.
	so we have to install with another command (ubuntu command)

sudo apt install python3-pip

i used this command, but it was not worked, it was showing apt not found, i used chatgpt instead of that command, i used this following command sudo yum install python3-pip

The first 2 command (below) not worked for me, so i just used the above command 
sudo yum install python3-pip

it was worked, & then I install my requrirments.txt file by using following commands
he using this following command 

run below command one by one
sudo apt-get update

sudo apt install python3-pip

 clear

 pip3 install -r requirements.txt


before run app.py we need to do some kind of settings

let see what settings we need to do right now


Go back to ec2 instance
in that ec2 instance, we have to some settings into this, so that we need to access the particular website from anywhere

so first, in lhs, just drag down, there is something called as security groups

    (i) click security group

	(ii) create security group

	security group name - FullAccess
	Description - FullAccess
(that is nothing but, any person can access this website from anywhere in this world)

now INBOUND RULES

just click add rule

	(i) type - choose for your req, like https, http, all traffic and all

	(ii) source - anywhere

after that 0.0.0.0 is available there, that is why we mention 0.0.0.0 is our app.

& then click create security group, once we create a security group, we can able to find our FullAccess in security group.

once we add the security group, which is on inbound rule, which is basically giving the permission for user to access and all we have to go back to our instance, 

just right click in our current instance, which is currently we are working with.

just right click it, 
select security & click on change security groups,
once we do this, then one new page will come, there just select our FullAccess name inside our associated security groups & click add security group & then just save it (click save).

now we have give the full access, now once we deploy it, we have to access our application from everywhere.

now I will go to my ubuntu back
and now I will write python3 app.py

	python3 app.py

now, it will start running, and we will get the api, that is http://0.0.0.0:8080/

but we will not able to access it 0.0.0.0, 
 
we have to use the url, in order to see that url, go back to instances, go and click on connect instance, and go ssh client, inside this ssh client, we have that public url

this will be your public domain server by default.

just copy this and go to google & paste it.
& at end just type :8080(because that is our default port number)

	(i) sudo apt-get update

	(ii) sudo apt install python3-pip

	(iii) clear

	(iv) pip3 install -r requirements.txt

	(v) python3 app.py


after completed, if you dont want, delete the instance & delete the security group.



