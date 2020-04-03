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

Then add following entry in your /etc/apt/sources.list

```
deb https://pkg.jenkins.io/debian-stable binary/
```

```
sudo apt-get update
sudo apt-get install jenkins
```
