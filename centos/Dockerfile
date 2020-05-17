FROM centos:8

ARG ROOT_PASSWORD=ansiblelab

RUN \
  yum -y install openssh-clients openssh-server && \
  yum -y clean all && \
  touch /run/utmp && \
  chmod u+s /usr/bin/ping && \
  echo "root:${ROOT_PASSWORD}" | chpasswd

# Allow root login in SSH
RUN sed -i 's/#PermitRootLogin/PermitRootLogin/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

COPY entrypoint.sh /

EXPOSE 22
ENTRYPOINT ["/entrypoint.sh"]