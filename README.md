# Maven Notes

<img width="900" alt="image" src="https://user-images.githubusercontent.com/49971693/166966273-9a4d1292-3b19-4950-bb07-99840823f6d1.png">

- To automate this build process, we use Maven.
- Maven is for java & build file is in XML Format
- Ant is also for Java and in XML format
- MSBuild for microsoft products
- Gradle - in Groovy fomat
- Make - builds executable programs and libs from source code


## Maven phases
- ![image](https://user-images.githubusercontent.com/49971693/166967063-807d1214-483b-4464-ac44-da3daf57ea31.png)
- mvn validate 
- mvn complie
- mvn test - need a unit test framework
- package - to JAR or WAR 
- verify
- install 

![image](https://user-images.githubusercontent.com/49971693/166967452-c6799b03-62c6-4eac-b173-12886abf34c9.png)

## Build Server on EC2 demo
1. Spinning up an EC2 instance referring to 
https://docs.aws.amazon.com/neptune/latest/userguide/iam-auth-connect-prerq.html and installing maven

```
sudo wget https://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
sudo yum install -y apache-maven
history
sudo yum install java-1.8.0-devel
sudo /usr/sbin/alternatives --config java
sudo /usr/sbin/alternatives --config javac
java -version
mvn -version
```
2. Referring to git repo devopshydclub/vprofile-repo, cloning it to practice maven
```
git clone https://github.com/devopshydclub/vprofile-repo.git
cd vprofile-repo
git checkout vp-rem
mvn test
```
<img width="383" alt="image" src="https://user-images.githubusercontent.com/49971693/166975613-483ed3f3-e69b-4353-a5df-1c4ab5dde36b.png">
Test reports are here
<img width="1091" alt="image" src="https://user-images.githubusercontent.com/49971693/166975931-a990b909-94fd-4f53-b6bd-2c37c2d87c55.png">

```
#  Will run all previous phases
mvn install
```


<img width="592" alt="image" src="https://user-images.githubusercontent.com/49971693/166976160-3f0cde2d-3106-4018-b190-16a0ec547a00.png">

The vprofile-v2.war is the artifact(artifact is the o/p of your build process)

<img width="592" alt="image" src="https://user-images.githubusercontent.com/49971693/166976476-1d6e0cd9-9284-4e0c-92ac-2dacff32cb59.png">
This is the dependency directory.

```
#  wipes out the target directory
mvn clean
```


```
# removes old and creates a new dir
mvn clean install
```


To install another version of mvn
```
wget https://archive.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
tar xzvf apache-maven-3.3.9-bin.tar.gz
sudo mv apache-maven-3.3.9 /opt/
/opt/apache-maven-3.3.9/bin/mvn -version
/opt/apache-maven-3.3.9/bin/mvn clean install
```
