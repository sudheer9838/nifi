sudo su
sudo yum update -y

install the latest docker engine package using this command 
sudo amazon-linux-extras install docker

sudo service docker start
sudo systemctl enable docker 

 execute Docker commands without using sudo.
 sudo usermod -a -G docker ec2-user
 
 getent group
 getent group docker 
 groups 
 docker info
 
  Build docker container with nifi image 
  docker pull apache/nifi:1.12.1
  
  Now we run the pulled image inside a container.
docker run --name nifi -p 8080:8080 -d apache/nifi:1.12.1 --restart=always 

docker exec -i -t nifi /bin/bash
echo "java.arg.8=-Duser.timezone=Asia/Colombo" >> conf/bootstrap.conf


Now go to the lib directory and get the following connectors as you wish.
cd lib
wget https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.23/mysql-connector-java-8.0.23.jar
wget https://repo1.maven.org/maven2/com/oracle/database/jdbc/ojdbc8/21.1.0.0/ojdbc8-21.1.0.0.jar
wget https://repo1.maven.org/maven2/org/apache/nifi/nifi-kite-nar/1.12.1/nifi-kite-nar-1.12.1.nar
wget https://s3.amazonaws.com/rds-downloads/rds-ca-2019-root.pem
wget https://jdbc.postgresql.org/download/postgresql-42.2.19.jar

Update the restart policy
docker update --restart=always nifi

To see Read the available restarting policies,
docker inspect -f "{{ .HostConfig.RestartPolicy }}" nifi
