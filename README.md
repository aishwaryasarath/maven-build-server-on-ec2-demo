# Maven Notes
[Maven Build Process](https://github.com/aishwaryasarath/maven-notes/blob/746b020bd7327e5ac42105440e8033e6db35ec4a/mavenBuildprocess.png)
- To automate this build process, we use Maven.
- Maven is for java & build file is in XML Format
- Ant is also for Java and in XML format
- MSBuild for microsoft products
- Gradle - in Groovy fomat
- Make - builds executable programs and libs from source code


## Maven phases
- [Phases](https://github.com/aishwaryasarath/maven-notes/blob/98b19ad25ac9f6b09a7bcdd79ba9fbc96ae02513/MavenPhases.png)
- mvn validate 
- mvn complie
- mvn test - need a unit test framework
- package - to JAR or WAR 
- verify
- install 

[Maven Life Cycle](https://github.com/aishwaryasarath/maven-notes/blob/f8cc9dfd1c0b881769660d361a3cc34585bae26b/MavenLifeCycle.png)

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
This is the dependency directory => /home/ec2-user/.m2/repository/

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
