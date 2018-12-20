FROM ubuntu:16.04
LABEL maintainer="lbarthon@student.42.fr"

# Updating default system
RUN apt-get update -y && apt-get upgrade -y
# Installing needed resources
RUN apt-get install -y wget openssh-server ca-certificates vim
# Installing postfix -- Email notifications
RUN apt-get install -y postfix
# Getting debian script to setup gitlab && installing it
RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && chmod +x script.deb.sh && ./script.deb.sh && apt-get install -y gitlab-ce
# Line to patch infinite loop when installing gitla
RUN apt-get install -y tzdata && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /script.deb.sh
# Expose web and ssh
EXPOSE 443 80 22
# Creating certificates
RUN mkdir -p /etc/gitlab/ssl/ && cd /etc/gitlab/ssl/ && openssl genrsa -out gitlab.domain.com.key 2048 && openssl req -new -x509 -key gitlab.domain.com.key -out gitlab.domain.com.crt -days 3650 -subj /CN=gitlab.domain.com
# Let's encrypt disabled -- Use our certificates
RUN echo "letsencrypt['enable'] = false" >> /etc/gitlab/gitlab.rb
# Setting gitlab ssh port
RUN echo "gitlab_rails['gitlab_shell_ssh_port'] = 22" >> /etc/gitlab/gitlab.rb
# Changing the external_url to an https one
RUN sed -i "s/^external_url.*/external_url \'https:\/\/gitlab.domain.com\'/" /etc/gitlab/gitlab.rb

# Commands to reconfigure and start the gitlab
RUN (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure
# Commands called when you docker run
# Starts both ssh and gitlab, tail to let it run.
# You can also run bash but it's not really usefull
ENTRYPOINT service ssh start && (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl start && tail -f /dev/null

# To build
# docker build -t ex03 .
# To run
# docker run --rm -it -p 80:80 -p 443:443 -p 2222:22 ex03
