FROM node:8

WORKDIR /var/src

# OS deps and awscli
RUN apt-get update -qq \
    && apt-get install -y curl zip python-pip python-dev build-essential \
    && pip install awscli

# Prevent `EMFILE: too many open files, scandir`
# https://stackoverflow.com/questions/8965606/node-and-error-emfile-too-many-open-files
RUN ulimit -Sn 65536
RUN echo "session required pam_limits.so" >> /etc/pam.d/common-session
RUN echo "root soft  nofile 40000" >> /etc/security/limits.conf
RUN echo "root hard  nofile 100000" >> /etc/security/limits.conf

# Allow the calling of npm bin scripts
RUN export PATH=$PATH:/var/src/node_modules/.bin

COPY docker-entrypoint.sh /usr/local/bin/
