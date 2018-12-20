FROM ruby
LABEL maintainer="lbarthon@student.42.fr"

# Updating & upgrading system
RUN apt-get update -y && apt-get upgrade -y
# Installing
RUN apt-get install -y build-essential libpq-dev nodejs sqlite3

# Copying ruby app
ONBUILD COPY ruby_app /opt/app
ONBUILD WORKDIR /opt/app

# Launching ruby app
ONBUILD RUN bundle install
ONBUILD RUN rake db:migrate
ONBUILD RUN rake db:seed
