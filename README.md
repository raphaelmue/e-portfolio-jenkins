# Jenkins e-Portfolio

## Content

## 1. Installation of Jenkins

### 1.1 Preconditions

This tutorial is only for an Ubuntu System. It is possible to install it on debian derivates as well, but the installation on windows might be slightly different.

Jenkins only supports Java 8. However, this does not mean that Jenkins does not support project that have Java 11.

### 1.2 Installation

First, the Jenkins repository must be added to the package manager `apt`:

```sh
wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add –
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```

Then update all repositories and install Jenkins with:

```sh
sudo apt update
sudo apt install jenkins
```

After installing Jenkins, its service should be start automatically. It is now accessable at [localhost](http://localhost:8080/). Anyways, you can checkm whether the Jenkins service is running with:

```sh
sudo systemctl status jenkins.service
```

This should print out something like this:

```sh
jenkins.service - LSB: Start Jenkins at boot time
  Loaded: loaded(/etc/init.d/jenkins; generated)
  Active: Active (excited) ...
```

If you are running Jenkins on a server, you might want to adjust your firewall, since otherwise you cat access Jenkins only from localhost:

```sh
sudo ufw allow 8080
sudo ufw status
```

### 1.3 Setting up Jenkins

Please apply the following steps:

1. Enter the initial admin password. This can be found at `/var/lib/jenkins/secrets/initialAdminPassword`. You need root rights to access the password.
1. Click on "Install suggested plugins".
1. Create an administrative user.
1. Configure Jenkins URL mapping.

Now you are ready to use Jenkins with its full possibilities.

## 2. Install Blue Ocean Plugin

If you want to install the Blue Ocean Plugin, just go to "Manage Jenkins" -> "Manage Plugins" -> Click on "Available" and search for "Blue Ocean". Tick the checkbox and press "Download now and install after restart".

After the restart, Jenkins is ready to use the Blue Ocean Plugin. Click on the link at the left navigation bar and you will enter Blue Ocean.

## 3. Create a GitHub Token

Open the GitHub website and go to Settings -> Developer Settings -> Personal Access Tokens and click "Generate new token". Then enter a token name and tick the following access rights for the token:

- repo
- read:org
- admin:repo_hook
- user:read
- user:email

Now copy the token (you will get to see the token only once).

## 4. Create a Pipeline

Please apply the following steps:

1. Enter Blue Ocean Jenkins
1. Click on "Create a Pipeline"
1. Click on GitHub
1. Enter your GitHub token
1. Select the user and the repository

If you already have a Jenkinsfile in your repository, your Jenkins job will be executed immediately. Otherwise you can create your Jenkinsfile via the UI of Blue Ocean by defining stages and steps.

Now you are ready to start 😉
