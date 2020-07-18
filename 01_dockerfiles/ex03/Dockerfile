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

ARG EXTERNAL_URL="192.168.99.101"

RUN mkdir -p /etc/gitlab/ssl && chmod 755 /etc/gitlab/ssl && \
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/gitlab/ssl/${EXTERNAL_URL}.key -out /etc/gitlab/ssl/${EXTERNAL_URL}.crt -subj "/C=RU/ST=Moscow/L=Moscow/O=21school/OU=docker-1/CN=${EXTERNAL_URL}" && \
	chmod 600 /etc/gitlab/ssl/* && \
	sed -i "s/\# letsencrypt\['enable'\] = nil/letsencrypt\['enable'\] = false/" /etc/gitlab/gitlab.rb && \
	sed -i "s/external_url 'http:\/\/gitlab.example.com'/external_url 'https:\/\/${EXTERNAL_URL}:443'/" /etc/gitlab/gitlab.rb


# RUN echo "external_url \"http://192.168.99.101\"" >> /etc/gitlab/gitlab.rb

EXPOSE 443 80 22

RUN mkdir -p /run/sshd

ENTRYPOINT (/opt/gitlab/embedded/bin/runsvdir-start &) && /usr/sbin/sshd && gitlab-ctl reconfigure && tail -f /dev/null

# docker build -t ex03 .
# docker run -it --rm -p 8080:80 -p 8022:22 -p 8443:443 --privileged ex03
#
# SSH CLONE
#	git clone ssh://git@192.168.99.100:8022/root/test.git
#
# HTTPS CLONE
# 	Отключаем проверку самоподписанного сертификата : git config --global http.sslVerify false
# 	git clone https://192.168.99.101:8443/root/test_project.git
