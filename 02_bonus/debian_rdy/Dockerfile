FROM debian:latest
LABEL maintainer="lbarthon@student.42.fr"

# Exposing ssh port
EXPOSE 22

# Updating & upgrading
RUN apt-get update -y && apt-get upgrade -y
# Installing default needed things
RUN apt-get install -y man vim git sudo openssh-server
# Making directory .ssh for user root
RUN mkdir -p /root/.ssh/
# Copying ssh key to user root
COPY id_rsa.pub /root/.ssh/authorized_keys
# Starting ssh service & tail to let it launched infinitely
CMD service ssh start && tail -f /dev/null

# To build, copy your ssh key here and then run
# docker build -t debian_rdy .
# To run
# docker run -p 2222:22 -d debian_rdy
# To ssh
# ssh -p 2222 root@$(docker-machine ip $DOCKER_MACHINE_NAME)
