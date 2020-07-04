FROM openjdk:8
RUN apt-get update && apt-get upgrade -y && apt-get install wget
RUN mkdir /server
COPY ./settings/* /server/
WORKDIR /server
RUN wget https://launcher.mojang.com/v1/objects/bb2b6b1aefcd70dfd1892149ac3a215f6c636b07/server.jar
RUN chmod 777 server.jar
ENTRYPOINT java -Xmx1024M -Xms1024M -jar server.jar nogui
EXPOSE 25565

#docker build -t minecraft-server .
#docker run -ti -p 25565:25565 -v serverfiles:/server minecraft-server
