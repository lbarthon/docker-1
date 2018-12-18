FROM debian

RUN apt-get update -y && apt-get upgrade -y && mkdir /opt/teamspeak/
RUN apt-get install -y bzip2
ADD https://files.teamspeak-services.com/releases/server/3.5.0/teamspeak3-server_linux_amd64-3.5.0.tar.bz2 ./
RUN tar xvfj teamspeak3-server_linux_amd64-3.5.0.tar.bz2
RUN mv teamspeak3-server_linux_amd64/* /opt/teamspeak/
RUN rm -rf teamspeak3-server_linux_amd64-3.5.0.tar.bz2 && rm -rf teamspeak3-server_linux_amd64/
RUN apt-get install -y ca-certificates
EXPOSE 9987/udp 30033/tcp 10011/tcp
CMD /opt/teamspeak/ts3server_minimal_runscript.sh license_accepted=1
