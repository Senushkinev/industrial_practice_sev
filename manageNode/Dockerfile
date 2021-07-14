FROM ubuntu:latest

RUN apt-get update 

RUN apt-get -y install openssh-server
RUN apt-get -y install python3


RUN echo root:1234 | chpasswd

COPY key/authorized_keys /root/.ssh/

EXPOSE 22

RUN mkdir /run/sshd
CMD /usr/sbin/sshd -D 
