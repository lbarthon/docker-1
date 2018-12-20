FROM debian
LABEL maintainer="lbarthon@student.42.fr"

# Setting env variable to accept ts3 license
ENV TS3SERVER_LICENSE=accept

# Setting default workdir
WORKDIR /root
# Update + upgrade
RUN apt-get update -y && apt-get upgrade -y
# Installing bzip to tar xvfj & wget
RUN apt-get install -y bzip2 wget
# Getting ts3
RUN wget https://files.teamspeak-services.com/releases/server/3.5.0/teamspeak3-server_linux_amd64-3.5.0.tar.bz2
# Unpacking ts3
RUN tar xvfj teamspeak3-server_linux_amd64-3.5.0.tar.bz2
# Workdir on folder untar
WORKDIR teamspeak3-server_linux_amd64
# Exposing ports
EXPOSE 9987/udp 30033 10011
# Running ts3server on docker run
ENTRYPOINT sh ts3server_minimal_runscript.sh
