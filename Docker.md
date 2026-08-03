#### what is Docker?
-Docker is tool that helps developers package an pplication along with everything it needs to run (code, libraries, settings, and dependencies)
into a single unit called a container.<br>
-Think of a conatiner as a portable box that conatain your application and everything required to run it.<br>
-This means the application will work the same way on your laptop, a server, or in the cloud<br>


1 docker ps
2  docker images
3docker pull nginx
    4  docker ps -a
    5  docker images -a
    6  docker run -itd --name newconatiner nginx
    7  docker ps -a

#### Installation 
sudo apt upadte <br>
sudo apt install docker.io -y  <br>
sudo systemctl start docker  <br>
sudo systemctl enable docker <br>
sudo systemctl status docker  <br>
docker ps  <br>
    2  docker ps  <br>
    3  docker pull nginx <br>
    4  nginx -v <br>
    5  docker run -itd newcontainer nginx <br>
    6  docker run -itd --name newcontainer nginx <br>
    7  docker ps -a <br>
    8* docker inspect newcontainer  <br>
    9*  <br>
   13  docker exec newcontainer /bin/bash  <br>
   14  ls <br>
   15  docker exec -it newcontainer /bin/bash <br>
