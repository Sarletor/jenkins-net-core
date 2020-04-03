# Jenkins with .NET Core

### Installing

Besides Jenkins you need to install Java 8 (11 available from jenkins 2.164). All others versions not supported.

###### Windows

**Java**
(https://www.oracle.com/java/technologies/javase-jre8-downloads.html)

**Jenkins**
(http://mirrors.jenkins-ci.org/windows-stable/latest)

###### Linux (Ubuntu 16.04)

**Java**

```
sudo apt-get update
sudo apt-get install default-jre
```

**Jenkins**

```
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```

Then add following entry in your **/etc/apt/sources.list**

```
deb https://pkg.jenkins.io/debian-stable binary/
```

Then finally install Jenkins:
```
sudo apt-get update
sudo apt-get install jenkins
```

### Configuration

After installing Jenkins will be available on localhost:8080

When you first start you will need to install plugins. 
Select **install suggested plugins** option. 
It contains most of needed plugins.


