FROM debian

ENV TS3SERVER_LICENSE=accept

WORKDIR /home/teamspeak

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y wget bzip2 && \
    wget  https://files.teamspeak-services.com/releases/server/3.12.1/teamspeak3-server_linux_amd64-3.12.1.tar.bz2 && \
    tar -xvf teamspeak3-server_linux_amd64-3.12.1.tar.bz2

WORKDIR teamspeak3-server_linux_amd64 
