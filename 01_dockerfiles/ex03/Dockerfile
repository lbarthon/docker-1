FROM ubuntu:16.04

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

RUN mkdir -p /etc/gitlab/ssl/ && cd /etc/gitlab/ssl/ && openssl genrsa -out gitlab.domain.com.key 2048 && openssl req -new -x509 -key gitlab.domain.com.key -out gitlab.domain.com.crt -days 3650 -subj /CN=gitlab.domain.com
RUN echo "letsencrypt['enable'] = false" >> /etc/gitlab/gitlab.rb
RUN echo "gitlab_rails['gitlab_shell_ssh_port'] = 22" >> /etc/gitlab/gitlab.rb
RUN sed -i "s/^external_url.*/external_url \'https:\/\/gitlab.domain.com\'/" /etc/gitlab/gitlab.rb

# Commands to reconfigure and start the gitlab
RUN (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure
# Launchs gitlab background + bash
ENTRYPOINT service ssh start && (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl start && bash
