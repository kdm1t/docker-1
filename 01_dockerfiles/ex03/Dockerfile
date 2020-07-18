FROM ubuntu:18.04

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y ca-certificates openssl openssh-server wget postfix

RUN wget https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh && \
	chmod 777 script.deb.sh && \
	./script.deb.sh && \
	apt-get install -y gitlab-ce

RUN apt update && apt install -y tzdata && \
	apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG EXTERNAL_URL="192.168.99.100"

RUN echo "external_url \"http://192.168.99.100\"" >> /etc/gitlab/gitlab.rb

EXPOSE 443 80 22

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && gitlab-ctl reconfigure && tail -f /dev/null

# docker build -t ex03 .
# docker run -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03
# how to clone with ssh:   ssh -T -p 8022 git@192.168.99.101
#                          git clone ssh://git@192.168.99.100:8022/root/test.git

# how to clone with https: git config --global http.sslVerify false
#                          git clone https://192.168.99.101:8443/root/test_project.git
#   	trusting_lewin
