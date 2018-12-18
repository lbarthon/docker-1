FROM ubuntu:14.04

# Updating default system
RUN apt-get update -y && apt-get upgrade -y
# Installing needed resources
RUN apt-get install -y curl openssh-server ca-certificates nano apt-transport-https
# Installing postfix -- Email notifications
RUN apt-get install -y postfix
# Expose web and ssh
EXPOSE 443 80 22
# Temp -- Setup bash
CMD bash
