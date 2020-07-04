#Version: 0.0.1
FROM	fedora:32
ENV	REFRESHED_AT 2020-05-19-1

RUN	dnf update -y

RUN 	dnf install -y glibc-langpack-en
RUN 	dnf install -y sudo iputils iproute iptables vim autofs rsync psmisc wget
RUN 	dnf install -y cifs-utils nfs-utils
RUN 	dnf install -y git gdb gcc python perl automake autoconf libtool flex bison
RUN	dnf install -y openssl-devel libxml2-devel python-devel libaio-devel libibverbs-devel librdmacm-devel readline-devel lvm2-devel glib2-devel userspace-rcu-devel libcmocka-devel libacl-devel sqlite-devel fuse-devel cups-devel dbus-devel docbook-style-xsl libarchive-devel libcap-devel libldb-devel libtalloc-devel libtdb-devel libtevent-devel libxslt openldap-devel pam-devel perl-ExtUtils-MakeMaker perl-Parse-Yapp perl-Test-Simple popt-devel python-tdb python-tevent quota-devel gnutls-devel libtirpc libtirpc-devel libnsl2-devel rpcgen jansson-devel python3-devel

RUN	dnf install -y glusterfs-api-devel glusterfs-devel
RUN	dnf install -y samba

RUN	echo "ALL  ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers.d/all

RUN	groupadd -g 4505 sprabhu
RUN	useradd -u4505 -g sprabhu sprabhu

RUN	useradd test1; (echo x; echo x)|smbpasswd -a test1
RUN	useradd test2; (echo x; echo x)|smbpasswd -a test2

RUN	mkdir /test; chmod 777 /test

COPY	smb.conf /etc/samba/smb.conf

USER	sprabhu:sprabhu
WORKDIR	/home/sprabhu

CMD	["/bin/bash"]
