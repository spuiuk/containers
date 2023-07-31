#Version: 0.0.1
FROM	fedora:38
ENV	REFRESHED_AT 2020-08-06-01

RUN	dnf update -y
RUN	dnf install -y git python3 make gcc gcc-c++ wget curl
RUN	ln -s /data/sprabhu/src /root/src
WORKDIR	/root/
