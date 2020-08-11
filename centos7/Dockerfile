FROM centos:7

RUN yum install -y openssh-clients openssh-server && \
    yum clean -y all && \
    echo "root:passwd" | chpasswd

RUN sed -i -e '/PermitRootLogin /d; $a PermitRootLogin yes' /etc/ssh/sshd_config && \
    sed -i -e '/PasswordAuthentication /d; $a PasswordAuthentication yes' /etc/ssh/sshd_config

RUN { \
       echo "LC_ALL=en_US.UTF-8"; \
       echo "LANG=en_US.UTF-8"; \
    } > /etc/environment

RUN ssh-keygen -A

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D", "-e"]
