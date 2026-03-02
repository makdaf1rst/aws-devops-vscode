<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Set Up a Web App in the Cloud

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-vscode)

**Author:** saqibh49@gmail.com  
**Email:** saqibh49@gmail.com

---

## Set Up a Web App Using AWS and VS Code

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_7a1de541)

---

## Introducing Today's Project!

In this project, I will demonstrate how to launch an EC2 instance, connect to it remotely using VS Code, and use Maven and Java to generate a basic web app. I'm doing this project to learn how developers set up remote development environments and build applications directly on cloud servers.

This project is part one of a series of DevOps projects where I'm building a CI/CD pipeline! I'll be working on the next project in about 12 hours, as soon as I get back from my day job!

I chose to do this project today because setting up development environments on remote servers is something I'll need to do as a cloud engineer, and getting comfortable with SSH, VS Code, and build tools like Maven now means I won't be fumbling with them later in a production setting.

### Key tools and concepts

Services I used were EC2, VS Code, Apache Maven, Amazon Corretto 8 (Java), and SSH. Key concepts I learnt include setting up key pairs for secure access, connecting to remote servers via SSH, using VS Code's Remote - SSH extension for remote development, generating Java web apps with Maven, and editing files through both an IDE and the terminal.

### Project reflection

This project took me approximately 2 hours. The most challenging part was establishing a connection with my EC2 via SSH. I ran into isssues multiple times, causing me to have to restart the project a few times. It was most rewarding to see my changes in the terminal reflect in my IDE because it felt like I actually did something instead of just playing around with cool new toys. 

One thing I didn't expect in this project was how fast I'd get comfortable with using terminal. I found that having to retype and re-examine commands to see where I went wrong or had a typo actually helped me get a feel for bash quicker than if I just copied and pasted in everything. 

---

## Launching an EC2 instance

### What I did in this step

In this step, I will launch a new EC2 instance, set up a key pair for secure access, and configure its network settings because these are the building blocks I need before I can connect to the instance remotely and start building my web app on it.

I started this project by launching an EC2 instance because this will be the remote server where I set up my development environment and build my web app — it's like having a computer in the cloud that I can connect to from anywhere.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_7852fbf3)

### I also enabled SSH

SSH is a secure protocol for connecting to a remote server, encrypting all the data sent between my computer and the server. I enabled SSH so that I can connect directly to my EC2 instance from my terminal and work on it as if I'm sitting right in front of it.

### Key pairs

A key pair is a way of securely connecting to an EC2 instance. It's made up of two parts — the public key stays with the instance and the private key stays with me. When I want to connect, the private key proves I'm authorized to access that specific machine, kind of like how only my house key can unlock my front door.

### Downloaded key pair file

Once I set up my key pair, AWS automatically downloaded the private key file to my computer. I need to keep this file safe because it's the only way I can prove I'm authorized to connect to my instance — if I lose it, I lose access.

---

## Set up VS Code

### What I did in this step

In this step, I will download and install VS Code, set up a terminal within it, and change the permissions on my .pem file because VS Code gives me a clean development environment to work from, and the .pem file needs the right permissions before I can use it to connect to my instance.

### What is VS Code?

VS Code is a code editor that makes writing and managing code way easier with features like syntax highlighting, extensions, and a built-in terminal. It's one of the most popular tools developers use, and in this project, I'll use it to connect to and work on my EC2 instance remotely.

I installed VS Code to have a proper development environment for connecting to my EC2 instance and building my web app. Working directly in a terminal is fine, but VS Code makes it much easier to write, edit, and manage code all in one place.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_53d05e68)

---

## My first terminal commands

A terminal is a text-based interface where I can type commands to interact with my computer or a remote server. The first command I ran for this project is cd ~/Desktop/DevOps, which navigates me to the folder on my desktop where I'm keeping my project files.

### Updating file permissions

I also updated my private key's permissions by running chmod 400 nextwork-keypair.pem, which restricts the file so only I can read it. This is required because SSH won't let me connect with a key file that's too open — it's a security measure to make sure nobody else on my machine can access the key.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_9328ada1)

---

## SSH connection to EC2 instance

### What I did in this step

In this step, I will connect to my EC2 instance because now that I have VS Code set up and my key permissions configured, I'm ready to actually SSH in and start working on the server.

### Connecting to EC2

To connect to my EC2 instance, I ran the command ssh -i ~/Desktop/DevOps/nextwork-keypair-3.pem ec2-user@ec2-3-148-232-28.us-east-2.compute.amazonaws.com, which uses my private key to securely log into the instance. Once connected, I can work on the server directly from my terminal as if I'm sitting right in front of it.

### This command required an IPv4 address

A server's IPv4 DNS is basically the public address of my EC2 instance on the internet. It's what I use to tell SSH where to connect — without it, my terminal wouldn't know which server to reach.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_e3069dca)

---

## Maven & Java

### What I did in this step

In this step, I will install Apache Maven and Amazon Corretto 8 (a version of Java) on my EC2 instance because these are the tools I need to generate and build my web app — Maven handles the project setup and dependencies, and Java is the language the app runs on.

### Why I'm using Maven

 Apache Maven is a build tool that helps set up, manage, and build Java projects. It handles things like creating the project structure, downloading dependencies, and packaging the app — so I don't have to do all of that manually.

Maven is required in this project because it's what I'll use to generate the skeleton of my web app and manage all the dependencies it needs to run. Without it, I'd have to set up the entire project structure and install each library by hand.

### Why I'm using Java

Java is a programming language that my web app is built on. I installed Amazon Corretto 8, which is Amazon's free, production-ready version of Java, because Maven and my web app both need Java to run.

Java is required in this project because it's the language my web app is written in — both Maven and the app itself depend on Java to compile and run, so without it, nothing works.

---

## Create the Application

### What I did in this step

In this step, I will run Maven commands to generate a Java web app because Maven can scaffold the entire project for me with one command — setting up all the folders, files, and configurations I need to get started.

### Creating the Java web app

I generated a Java web app using the command mvn archetype:generate, which tells Maven to create a new project based on a template. The flags I included define the project's group ID (com.nextwork.app), the project name (nextwork-web-project), the template to use (maven-archetype-webapp), and set interactive mode to false so Maven just builds it without asking me a bunch of questions along the way.

### Installing Remote - SSH

I installed Remote - SSH, which is a VS Code extension that lets me connect directly to a remote server and work on its files as if they're on my local machine. I installed it to make editing my web app's code on my EC2 instance way more convenient than typing everything out in the terminal.

### SSH configuration details

Configuration details required to set up a remote connection include the host name (a friendly name for the connection), the hostname (my EC2 instance's public IPv4 DNS), the user (ec2-user), and the path to my private key file so VS Code can authenticate with my instance.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_2939cf01)

---

## Create the Application

### Exploring the project structure

Using VS Code's file explorer, I could see the full structure of my web app project on my EC2 instance, including the pom.xml file which contains all the project's configuration — things like the group ID, artifact ID, version, dependencies like JUnit for testing, and build settings. Being able to browse and edit these files visually in VS Code is so much easier than navigating through the terminal.

Two of the project folders created by Maven are src and webapp, which make up the core of my web app. The src folder is where all the source code lives, and the webapp folder contains the web-facing files like the index.jsp page that users actually see when they visit the app.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_45f91fd7)

---

## Using Remote - SSH

### What I did in this step

In this step, I will install a VS Code extension to set up a remote SSH connection to my EC2 instance so I can browse and edit my web app's files directly in VS Code. This is way easier than editing files through the terminal because I get a full visual editor with all of VS Code's features.

### Updating the web app

The index.jsp is the default web page for my app — it's basically the homepage that gets displayed when someone visits the site. JSP stands for JavaServer Pages, which lets you mix HTML with Java code to create dynamic web content.

I edited index.jsp by adding my name to the <h1> tag, so it says Hello Saqib! instead of Hello World!, then I added a line with a <p> tag with some paragraph text inside introducing my project. 

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_7a1de541)

---

## Using nano

### Additional improvements

In this secret mission, I will edit index.jsp directly from the terminal instead of using VS Code because it's good to know how to make quick edits without relying on an IDE — especially in situations where VS Code or a remote connection isn't available.

### Terminal vs IDE

An alternative to using IDEs is using terminal. To edit index.jsp, I ran the command nano index.jsp. 

Compared to using an IDE, editing index.jsp in the terminal felt easier, since instead of managing hosts, mutliple windows and worrying about connection issues, I just ran single command and I was in my file  I'd be more likely to use an IDE if there weren't so many steps to get set up, even more so if connection issues weren't so prevalent. 

### Verifying my work

To verify my editing work in the terminal, I checked my SSH window to see if the changes showed there as well. It was possible to see my changes in VS Code right away because VS Code is connected to the same EC2 instance through Remote - SSH, so any changes I make in the terminal are reflected in VS Code instantly since they're both looking at the same files.

![Image](http://learn.nextwork.org/grateful_white_lucky_bat/uploads/aws-devops-vscode_a3324ad41)

---

---
