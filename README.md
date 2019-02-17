# Install Jenkins on AWS EC2
Jenkins is a self-contained Java-based program, ready to run out-of-the-box, with packages for Windows, Mac OS X and other Unix-like operating systems. As an extensible automation server, Jenkins can be used as a simple CI server or turned into the continuous delivery hub for any project.

### Follow this article in **[Youtube](https://youtu.be/QhoiJ5D3SKM)**

### Launch Instance
1. EC2 RHEL 7.x Instance
   - With Internet Access
   - Security Group with Port `8080` open for internet

#### Notes
1. Make sure Java v1.8.x is installed
```sh
java -version
```
2. Use sudo when needed

### SSH Into instance
SSH into your instance
```sh

chmod 400 youtube-test.pem

ssh ssh -i "youtube-test.pem" ec2instanceurl

```

### Install Java
We will be using open java for our demo, Get latest version from http://openjdk.java.net/install/
```sh
yum install java-1.8*
```

### Confirm Java Version
Lets install java and set the java home
```sh
java -version
```
_The output should be something like this,_
```
[root@~]# java -version
openjdk version "1.8.0_151"
OpenJDK Runtime Environment (build 1.8.0_151-b12)
OpenJDK 64-Bit Server VM (build 25.151-b12, mixed mode)
```

## Install Jenkins
You can install jenkins using the rpm or by setting up the repo. We will setup the repo so that we can update it easily in future.
Get latest version of jenkins from https://pkg.jenkins.io/redhat-stable/
```sh
yum -y install wget
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
yum -y install jenkins
```

### Start Jenkins
```sh
# Start jenkins service
systemctl start jenkins

# Check jenkins status

systemctl status jenkins

# Setup Jenkins to start at boot,
systemctl enable jenkins
```

#### Accessing Jenkins
By default jenkins runs at port `8080`, You can access jenkins at
```sh
http://YOUR-SERVER-PUBLIC-IP:8080
```
#### Configure Jenkins
- The default Username is `admin`
- Grab the default password 
  - Password Location:`/var/lib/jenkins/secrets/initialAdminPassword`
- `Skip` Plugin Installation; _We can do it later_
- Change admin password
  - `Admin` > `Configure` > `Password`
- Configure `java` path
  - `Manage Jenkins` > `Global Tool Configuration` > `JDK`  
- Create another admin user id

### Test Jenkins Jobs
1. Create “new item”
1. Enter an item name – `My-First-Project`
   - Chose `Freestyle` project
1. Under Build section
	Execute shell : echo "Welcome to Jenkins Youtube"
1. Save your job 
1. Build job
1. Check "console output"

### Next Step
- [] [Configure Users & Groups in Jenkins]()
- [] [Secure your Jenkins Server]()
- [] [Jenkins Plugin Installation]()
- [] [Jenkins Master-Slave Configuration]()
- [ ] Setup Jenkins to run inside Tomcat Server
