FROM debian:latest
LABEL maintainer="lbarthon@student.42.fr"

# Expose server port
EXPOSE 25565

# Update and upgrade, as always
RUN apt-get update -y && apt-get upgrade -y
# Install needed packages
RUN apt-get install -y default-jdk git sudo
# Copy server files
COPY ./server/ /root/server/
# Workdir on server
WORKDIR /root/server/
# Run spigot server
CMD java -Xms1G -Xmx1G -XX:+UseConcMarkSweepGC -jar spigot.jar

# To build
# docker build -t spigot .
# To run
# docker run --restart always -d -p 25565:25565 spigot
