#### what is Docker?
-Docker is tool that helps developers package an pplication along with everything it needs to run (code, libraries, settings, and dependencies)
into a single unit called a container.<br>
-Think of a conatiner as a portable box that conatain your application and everything required to run it.<br>
-This means the application will work the same way on your laptop, a server, or in the cloud<br>

#### Installation 
sudo apt upadte <br>
sudo apt install docker.io -y  <br>
sudo systemctl start docker  <br>
sudo systemctl enable docker <br>
sudo systemctl status docker  <br>
docker ps  <br>
docker ps  <br>
docker pull nginx <br>
nginx -v <br>
docker run -itd newcontainer nginx <br>
docker run -itd --name newcontainer nginx <br>
docker ps -a <br>
docker inspect newcontainer  <br>
<br>
   13  docker exec newcontainer /bin/bash  <br>
   14  ls <br>
   15  docker exec -it newcontainer /bin/bash <br>
