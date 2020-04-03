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

Next you will need to **CREATE** admin user.

###### Then you need to install additional plugins

1. Select 'Manage Jenkins'
2. Select 'Manage Plugins'
3. Select 'Available' tab

You need to install these plugins:
1. Bitbucket plugin (https://plugins.jenkins.io/bitbucket/)
2. NodeJS plugin (https://plugins.jenkins.io/nodejs/)

###### Then return back to 'Manage Jenkins' and select 'Global Tool Configuration'.

Find NodeJS section and select needed version for using (for example 10.15.0)

After that all ready to create new jenkins job.

# Using

1. Select 'New Item'
2. Select 'Freestyle project' (it is enough for our requirements)
3. Select job 'Settings'
4. In 'Source Code Management' section you need to select git repository and write branch name
5. In 'Build Triggers' section you need to check 'Build when a change is pushed to BitBucket' option
6. In 'Build Environment' section you need to select NodeJS version. Other options don't change
7. In 'Build' section you need to add new step:
  7.1 Execute Shell (Linux)
  7.2 Execute Windows batch command (Windows)
  
  Then paste this script:
  ```
  cd src/WebSite/ClientApp
  npm install --registry https://npm.entrypoint.lv
  cd ../../Website.Tests
  dotnet test -v=normal
  cd ../../
  sudo systemctl stop kestrel-starter.com.service
  dotnet publish --configuration release
  cd ~
  rsync -r /var/lib/jenkins/workspace/Stage/src/WebSite/bin/Release/netcoreapp3.0/publish/ /var/aspnet/starter.com
  sudo systemctl start kestrel-starter.com.service
  ```
  
8. For automated build you need to create webhook in your bitbucket repository with jenkins URL: localhost:8080/bitbucket-hook/
