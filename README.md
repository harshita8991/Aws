# Aws
<h1><b>1.Making an account on AWS</b></h1>
1.Go to ["https://aws.amazon.com/resources/create-account"] and follow the instructions

<h1><b>Starting an EC2 instance</b></h1>
1. On the AWS dashboard, search for EC2 and click EC2<br><br>
<img src="https://github.com/user-attachments/assets/b7e4434a-9508-4689-b977-ce510a18a2ae" height="350"><br><br>
2.Click Launch Instance<br>
<br>
<img src="https://github.com/user-attachments/assets/dcda92ae-be51-4e4f-9666-b5c0e69d8bf6" height="350">
<br><br>
3.Type your server name and choose the OS you desire (We are choosing Ubuntu for this tutorial)<br><br>
<img src="https://github.com/user-attachments/assets/b62a061b-e42e-4220-8169-168f8bcd55d6" height="350"><br><br>
4.In the "Key Pair" section click on "Create new key pair"<br><br>
<img src="https://github.com/user-attachments/assets/807e5b20-434e-4c81-b5c1-121f6d0bf30c" height="350"><br>
<br>
5. Name your key pair and click on .ppk and then create new key (The key pair will get downloaded)<br><br>
<img src="https://github.com/user-attachments/assets/928dbfce-9039-4185-a67c-0c132c27df33" height="350"><br><br>
6. In the network section click on "Allow HTTP traffic from the internet"<br><br>
<img src="https://github.com/user-attachments/assets/568ba0ce-8acc-4621-8f46-933f36f28af5"height="350"><br><br>
7. Finally click on "Launch Instance"<br><br>
<img src="https://github.com/user-attachments/assets/8895b2d5-5da8-4b97-b850-9451c10834c3" height="350"><br><br>

# 2. using EC2 in aws

**First open aws search EC2 then Launch Instance and there select keypair in putty or pem then download it**

### By using pem file for linux
```
ssh -i /path/to/your/pemfile.pem ec2-user@your-ec2-public-ip
```


### By using putty

**after that Launch it and run putty and paste public id on HOST NAME and open that downloaded key pair for putty in SSH then Auth then Credentials and open there**

**after that run it and write username as ubuntu as selected os and then type following commands**


```
sudo apt update
```

```
sudo apt install apache2
```
**to install a web server on ip then**

```
sudo su
```
 **for convert $ into # for getting admin role then**

```
cd /var/www/html/
```
   
   **then**

```
ls
```
  **for list of html file in it**

**then copy that html file name and write**
```
rm index.html
```
**rm means remove command**

```
vi index.html
```
 **this will open a notepad like and write html code there like (vi is editor) -**

![Screenshot 2024-09-10 225017](https://github.com/user-attachments/assets/ae2e7ceb-b9e6-4f82-a7ff-80b2bc47861c)




**then press ctrl+c then shift+colon then write wq and enter**

**now copy your public ip and paste it on browser you will see the texts written by you (by using html above)**


# 3. USING CONTAINER IN VM and adding nginx server by Docker

**First open aws search EC2 then Launch Instance and there select keypair in putty then download it**

**after that edit network setting and click on add security group rule and select TCP,UDP,ALL TRAFFIC AND SELECT EVERYWHERE SOURCE TYPE IN THEM then Launch it and run putty and paste public id on HOST NAME and open that downloaded key pair for putty in SSH then Auth then Credentials and open there**

**after that run it and write username as ubuntu as selected os and then type following commands**
```
curl -sL https://github.com/ShubhamTatvamasi/docker-install/raw/master/docker-install.sh | bash
```
**this will install and run docker in your vm**

```
newgrp docker
```
**this command will help us to use docker**

```
docker ps
```
**this will list docker**

```
docker --version
```
**this will display the version of docker installed**

### now installing nginx

```
docker pull nginx
```
**You can download Nginx from a pre-built Docker image, with a default Nginx configuration, by above command.
This downloads all the necessary components for the container.**

```
docker run --name docker-nginx -p 80:80 nginx
```
**Nginx installed, you can configure the container so that it’s publicly accessible as a web server.**

**run is the command to create a new container**

**The --name flag is how you specify the name of the container. If left blank, a generated name like nostalgic_hopper will be assigned.**

**-p specifies the port you are exposing in the format of -p local-machine-port:internal-container-port. In this case, you are mapping port :80 in the container to port :80 on the server.**

**nginx is the name of the image on Docker Hub.**


### now this will show this on your public ip
![Screenshot 2024-09-17 185925](https://github.com/user-attachments/assets/bb2255a5-8c0b-4d5b-81ee-a1c6a552f5da)



#### In your terminal, enter CTRL+C to stop the container from running.


```
docker ps -a
```
**verify the container status with this command**

```
docker rm docker-nginx
```
**Remove the existing  container**

```
docker run --name docker-nginx -p 80:80 -d nginx
```
**Create a new, detached Nginx container,By attaching the -d flag, you are running this container in the background.**


```
docker ps
```
**this will obtain info about your container**


```
docker stop docker-nginx
```
**Stop the container**


```
docker rm docker-nginx
```
**remove the container**


## Building a Web Page to Serve on Nginx


```
mkdir -p ~/docker-nginx/html
```
**Create a new directory for your website content within the home directory**


```
cd ~/docker-nginx/html
```
**by this you navigate into this**


```
vi index.html
```
**now press i and write your code in html like**

![Screenshot 2024-09-10 225017](https://github.com/user-attachments/assets/ae2e7ceb-b9e6-4f82-a7ff-80b2bc47861c)

**then press ctrl+c then shift+colon then write wq and enter**


```
docker run --name docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx
```
**Linking the Container to the Local Filesystem**

**open your public ip in browser you will see as the content as  your html code**


## Using Your Own Nginx Configuration File

```
cd ~/docker-nginx
```

```
docker cp docker-nginx:/etc/nginx/conf.d/default.conf default.conf
```
**Copy the Nginx config directory into your project folder**



```
docker stop docker-nginx
```


```
docker rm docker-nginx
```
**to rebuild the container stop the container then remove it**



```
docker run --name docker-nginx -p 80:80 -v ~/docker-nginx/html:/usr/share/nginx/html -v ~/docker-nginx/default.conf:/etc/nginx/conf.d/default.conf -d nginx
```
**This command links the custom website pages to the container.**




```
docker restart docker-nginx
```
**you need to restart your container to reflect changes  on the associated pages.**





