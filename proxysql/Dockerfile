#Pour la mise en place sur docker, de proxysql et un MySQL Group Replication avec deux noeuds
#Une image contenant proxysql va être créé pour Group Replication, une image officiel mysql sera utilisé

#/Docker file pour l'image proxysql:
FROM debian:latest
#copy proxysql to /tmp
COPY proxysql_1.3.3-debian8_amd64.deb /tmp 
#expose default proxysql port
EXPOSE 6033
#install proxysql
RUN dpkg -i /tmp/proxysql_1.3.3-debian8_amd64.deb
#remove deb file
#RUN rm -rf /tmp/proxysql_1.3.3-debian8_amd64.deb
#install openssl needed for proxysql, and mysql for administration purposes only
RUN apt-get update
RUN apt-get --assume-yes install openssl
RUN apt-get --assume-yes install mysql-client
RUN mkdir /etc/proxysql
#move configuration file to new volume
RUN mv /etc/proxysql.cnf /etc/proxysql/proxysql.cnf 
#store configuration on volume accessible to host, always after setting content
VOLUME /etc/proxysql
#main process, launch it in foreground with default conf file in the new path
ENTRYPOINT ["/usr/bin/proxysql", "--foreground", "-c", "/etc/proxysql/proxysql.cnf"]

#PS C:\Users\nicolas.moreau> docker build -t "proxysql:1.3.3" .