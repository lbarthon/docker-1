FROM alpine
LABEL maintainer="lbarthon@student.42.fr"

# Update sources && upgrade && install vim
RUN apk update && apk upgrade && apk add vim
# Launch vim when run
ENTRYPOINT vim

# To build
# docker build -t ex00 .
# To run
# docker run --rm -it ex00
