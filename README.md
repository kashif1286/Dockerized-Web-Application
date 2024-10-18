
#  Dockerized Web Application


![Blank diagram](https://github.com/user-attachments/assets/4a8aa221-b738-4375-b02d-aa78605c97e4)


Description: Develop a microservice-based web application using Docker containers on EC2.

Tools/Technologies: Docker, AWS EC2,  Linux.

Highlights: Demonstrates microservices architecture, containerization, and automation of deployment.

# STEP 1.

setup ec2 

click a ec2

![ec1](https://github.com/user-attachments/assets/1e6ce706-69a5-4f3f-a893-1148cf782753)


launch a EC2 instnace 

![ec2](https://github.com/user-attachments/assets/35672aa3-2513-4edd-8c35-f166bc037291)

give a name and tag .

choose Linux amazon machine image (ubuntu).

![ec3](https://github.com/user-attachments/assets/5250f5c1-b863-43b3-8780-332ee5256200)

take free tier eligible (t2 micro).

and selesct a keypair or create an new key pair .


![ec4](https://github.com/user-attachments/assets/120da240-bce1-4660-98f7-5399ecf33951)

put a defualt vpc and Enable auto-assign public IP.

and crete a new security group.

![ec5](https://github.com/user-attachments/assets/9f789150-1979-4d64-b33b-4df4b06fc268)

taking a fout inbound rule for website 

1. ssh

2. http

![ec6](https://github.com/user-attachments/assets/8d7cfa43-7d02-43b0-8864-12b5496cfc01)

3. custom  tcp and give a port range for custom tcp (3000) 

4. https

lunch instnace 

![ec7](https://github.com/user-attachments/assets/7e4ca862-e4cc-4a9c-b17e-2c4195232645)



# Step 2: Set Up Your Development Environment

cheak a running instnace cheak a status.

![rn1](https://github.com/user-attachments/assets/75026bbc-6497-49f7-9638-2eb9521f6b29)

connect to the instnace for terminal 

![rn2](https://github.com/user-attachments/assets/41827d9d-c29c-486b-b82d-a349a52f4ca5)


for linux 

Open a terminal window.

Update your package index.

```bash
sudo apt-get update

```
![rn3](https://github.com/user-attachments/assets/2cdc36ad-dd6b-4cea-8508-ebcda250f639)


```bash
sudo su

```

![rn4](https://github.com/user-attachments/assets/58eab47a-0b56-4bc9-b438-c3586ab78246)

Install the necessary packages

```bash
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common


```

![rn5](https://github.com/user-attachments/assets/270da557-502d-442e-883f-9e8b262116af)

give only   ( y = yes)   for continue

![rn6](https://github.com/user-attachments/assets/67283cda-5e24-4cf5-af8e-e2ad28c22990)

Add Docker’s GPG Key Manually

Use the new method to download Docker's GPG key and store it in a keyring. This avoids the deprecated apt-key command:


```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg


```

![rn7](https://github.com/user-attachments/assets/0ef87672-4d74-4513-a53d-96602abc6850)

Update the Docker Repository with the Correct GPG Key

Next, update the Docker repository configuration to point to the new key location:

```bash
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu focal stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null


```


![rn8](https://github.com/user-attachments/assets/822cc755-00ca-49ec-a02c-adc393467963)

Clean the Apt Cache and Update Again

Clear the cache and try updating the package list again:

```bash
sudo apt-get clean
sudo apt update

```


![rn9](https://github.com/user-attachments/assets/9f302c41-52a7-4a0b-9dd6-81416e56a9bf)

Install Docker Packages

After the update, try installing Docker again:

```bash
sudo apt install docker-ce docker-ce-cli containerd.io

```

![rn10](https://github.com/user-attachments/assets/79c72c17-5a45-40b8-bd20-9986fe235d18)

you will giving a ( y = yes) for continue

![rn10 1](https://github.com/user-attachments/assets/17d11b08-7380-443d-9da2-a8a6e5b1d5a0)

Start Docker Service:

Start the Docker service

```bash
sudo systemctl start docker
```

![rn11](https://github.com/user-attachments/assets/5914597b-70f1-4687-a254-469cdc8824d8)

To enable Docker to start on boot

```bash
sudo systemctl enable docker

```

![rn12](https://github.com/user-attachments/assets/7883cda5-247a-4c31-b61f-2261abb06bda)

Verify Installation:

Run the command

```bash
docker --version
```

![rn13](https://github.com/user-attachments/assets/51326217-27ad-43b9-b66a-3c3d881cf773)

Install AWS CLI

For Linux:

You can use the following command

Download the AWS CLI Installer:

Use the following command to download the AWS CLI installation script:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

```

![rn14](https://github.com/user-attachments/assets/1a9ed23b-1f50-47cc-b87e-c7bcd156ff7f)

Unzip the Downloaded File:

You’ll need to unzip the file. Install unzip if it’s not already installed, and then unzip the package:

```bash
sudo apt-get install unzip
unzip awscliv2.zip


```

![rn15](https://github.com/user-attachments/assets/874d53e1-0afc-4762-b269-3a004b2a99ee)

Run the Installer:

After unzipping, run the installer:

```bash
sudo ./aws/install

```

![rn16](https://github.com/user-attachments/assets/92499db8-0449-46b2-956b-31acdd870740)

Verify the Installation:

Check if the AWS CLI is installed correctly by running:

```bash
aws --version


```

![rn17](https://github.com/user-attachments/assets/6cb1b199-2378-44cf-90dc-4f6571f2cdea)

# Step 3 create and setup acces key 

go to IAM (identity Accses managment) click a user

![iam1](https://github.com/user-attachments/assets/773c1515-200c-4a50-83c9-e8b18a3ef184)

create user user.

Add a user name.

![iam2](https://github.com/user-attachments/assets/280b3012-017d-41e7-8a76-74ad3497836f)


Add a user name.

![iam3](https://github.com/user-attachments/assets/1a2ce75e-06d5-4bc5-be77-727d9ab2eb56)


set permistion and attached policy directly. 

![iam4](https://github.com/user-attachments/assets/dde92552-2059-4bc6-9cfa-bd440304311f)

and create usr

![iam5](https://github.com/user-attachments/assets/73866f68-7500-449c-9929-37c88fd10a29)

click a create user name and go to security credentials.

![iam6](https://github.com/user-attachments/assets/117852ba-99a8-4b88-a4c3-affff1fd1805)

create access key for aws config

![iam7](https://github.com/user-attachments/assets/5b493520-b6bd-4fe3-b9a1-14aa1e13605a)

click a command line (CLI)


click last butoon .




![iam8](https://github.com/user-attachments/assets/24779700-70d4-48c5-bb6d-b94d7f8d0009)

name user key and crete acces key 

![iam9](https://github.com/user-attachments/assets/6f6f4de6-e076-418e-a6c8-54f79e671ce7)

generet ACCESS key and Secret Access key  and download .csv file for nedeed

![iam10](https://github.com/user-attachments/assets/f5a3f9ac-9bd0-4a0d-808d-efc2e7e92544)


# Step 4: Develop Your Microservice Application

Configure AWS CLI
Run Configuration Command:

In your terminal or command prompt, run

```bash
aws configure
```

Enter Your Credentials:


![fn1](https://github.com/user-attachments/assets/875e29ff-2c40-4b07-bcb9-98ed98e12b92)

COPY A ACCESS KEY FROM CRETED I AM USER AND PASTE.

AWS Access Key ID: (Enter your AWS access key)

![fn2](https://github.com/user-attachments/assets/f2d175f6-16a6-4088-8313-c0abeea16c68)


COPY A  SECERET ACCESS KEY FROM CRETED I AM USER AND PASTE.

AWS Secret Access Key: (Enter your AWS secret access key)

![fn3](https://github.com/user-attachments/assets/25345cc8-3dcc-47ff-9a33-217acfb1869a)

Default region name: (Enter your preferred AWS region, e.g., 
us-east-1, us-west-2, etc.)

Default output format: (You can enter json, text, or table. json is recommended.)

![fn4](https://github.com/user-attachments/assets/cdeabd96-87c2-4db9-82af-79c255404c9a)

Create a Sample Application
1.1. Set Up Project Directory

Open your terminal.
Create a new directory for your microservice

```bash
mkdir my-microservice
cd my-microservice

```

![fn5](https://github.com/user-attachments/assets/317a1809-816d-435c-a820-97becc77c10e)

Create the Application Files

Create app.js File:

In your project directory, create a file named app.js

```bash
nano app.js

```

![fn6](https://github.com/user-attachments/assets/1b226367-57e7-480d-924a-297daee17194)

Add Code to app.js:

Open app.js in your favorite text editor and add the following code:

```bash
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
    res.send('Hello from Dockerized Microservice!');
});

app.listen(port, '0.0.0.0', () => {
    console.log(`App running at http://localhost:${port}`);
});

```

and save Ctrl + X = y

![fn7](https://github.com/user-attachments/assets/651b02ae-86f4-4f96-912a-2e59102e66a1)

Create package.json File:

In your project directory, create a file named package.json

```bash
nano package.json


```


![fn8](https://github.com/user-attachments/assets/53eb7107-8d1d-42f1-af69-a5c2994a163e)

Add Code to package.json:

Open package.json in your text editor and add the following code:

```bash
{
  "name": "my-microservice",
  "version": "1.0.0",
  "main": "app.js",
  "dependencies": {
    "express": "^4.17.1"
  },
  "scripts": {
    "start": "node app.js"
  }
}



```


![fn9](https://github.com/user-attachments/assets/d337e2ad-1c19-4286-aa7c-68ce2aa5998b)

Create a Dockerfile

2.1. Create the Dockerfile

In your project directory, create a file named Dockerfile (no file extension)


```bash
nano Dockerfile

```

![fn10](https://github.com/user-attachments/assets/e91025b2-7be7-4d03-8f3c-5aff4b994a99)

Add Instructions to the Dockerfile:

Open the Dockerfile in your text editor and add the following code

```bash
# Use the official Node.js image as the base image
FROM node:14

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port the app runs on
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]


```

![fn11](https://github.com/user-attachments/assets/0666cd3c-8d9f-45d6-8a54-f6c6bfdea706)

Build the Docker Image

3.1. Build the Image:

Make sure you're still in the my-microservice directory.

Run the following command to build the Docker image:

```bash
docker build -t my-microservice .

```

Explanation:
docker build: This command builds an image from the Dockerfile.

-t my-microservice: This tags the image with the name my-microservice.

.: This indicates the current directory should be used for the build context.

Wait for the Build Process to Complete:

The output will show the steps taken in the Dockerfile. If successful, you’ll see a message like Successfully built <image_id>.

![fn12](https://github.com/user-attachments/assets/d9176c99-8664-4e88-b637-22aeaa0e91d5)

Run the Docker Container Locally
4.1. Run the Container:

To run your Docker container, execute the following command

```bash
docker run -p 3000:3000 my-microservice


```

Explanation:
docker run: This command creates and starts a container from the specified image.

-p 3000:3000: This maps port 3000 on your host to port 3000 in the container.

my-microservice: This specifies the image to run.

![fn13](https://github.com/user-attachments/assets/3aca20e1-c453-412a-884b-6c7d21774769)
 Access Your Application:

Open your web browser and navigate to

```bash
http://localhost:3000
```
localhost = copy your running insnace id 
paste website 

![fn14](https://github.com/user-attachments/assets/ace476d6-d3f6-43a5-9b10-d9749f8295b3)

cheak a website your project is run

Hello from Dockerized Microservice!


![fn15](https://github.com/user-attachments/assets/7bcd4f44-67dc-421d-a0ad-ad9a0b9e10dc)

configuration your project is successful.

after successful your project you deleted and termineted service .


#   M y   N e w   R e p o s i t o r y 
 
 
