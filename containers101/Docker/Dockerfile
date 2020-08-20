#Pull base image
FROM ubuntu

#Add timezone to resolve issue with later ubuntu versions in docker
ENV TZ=Europe/London
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#Install Apache
RUN apt-get update -y && apt-get install apache2 apache2-utils -y

#Define default port
EXPOSE 80

#Define default command
ENTRYPOINT [ "/usr/sbin/apache2ctl" ]

#Define default arguments
CMD [ "-D", "FOREGROUND" ]
