# trên macOS and Linux
1. Open Terminal
2. Create a bridge network trong docker bằng lệnh:
   `docker network create jenkins`
3. download and run image docker:dind
   `docker run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --publish 2376:2376 docker:dind --storage-driver overlay2`
4. 
  - Tạo dockerfile:
    `FROM jenkins/jenkins:2.332.2-jdk11
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.25.3 docker-workflow:1.28"`
- build dockerfile vừa tạo ra image mới
  `docker build -t myjenkins-blueocean:2.332.2-1 .`

5. run container from image vừa tạo ở trên:
   `docker run --name jenkins-blueocean --rm --detach --network jenkins --env DOCKER_HOST=tcp://docker:2376 --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 --publish 8080:8080 --publish 50000:50000 --volume jenkins-data:/var/jenkins_home --volume jenkins-docker-certs:/certs/client:ro myjenkins-blueocean:2.332.2-1`



6. truy cập vào container vừa tạo bên trên bằng câu lệnh:
   `docker exec -it jenkins-blueocean bash`
7. có thể xem logs của container trên bằng lệnh:
   `docker logs jenkins-blueocean`

8. Unlocking jenkins
   - Mở trình duyệt rồi truy cập vào địa chỉ:
    **`http://localhost:8080`**
![unlock](setup-jenkins-01-unlock-jenkins-page.jpg "images unlock jenkins")

   - lấy password từ câu lệnh sau:
    `docker exec -it jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword`
    - copy password đó
    - trên trang unlock jenkins, paste password trên vào trường Administrator password và click continue.





