FROM rhel7

MAINTAINER docker@softwarecollections.org

RUN yum update -y && yum install -y yum-utils && \
    yum-config-manager --enable rhel-server-rhscl-7-rpms && \
    yum-config-manager --enable rhel-7-server-optional-rpms && \
    yum clean all

RUN yum install -y --setopt=tsflags=nodocs mysql55 hostname && yum clean all


EXPOSE 3306
ENV HOME            /var/lib/mysql
ENV BASH_ENV        /etc/profile.d/cont-env.sh
ADD ./.bashrc $HOME/.bashrc
ADD ./usr /usr
ADD ./my.cnf /opt/rh/mysql55/root/etc/my.cnf
ADD ./enablemysql55.sh /usr/share/cont-layer/common/env/enablemysql55.sh
ADD ./etc /etc
ADD ./root /root

RUN	/usr/libexec/cont-setup && \
	:

USER mysql

VOLUME ["/var/lib/mysql/data"]

CMD ["cont-mysqld"]

