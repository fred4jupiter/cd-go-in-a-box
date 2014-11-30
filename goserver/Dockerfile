FROM dockerfile/java
MAINTAINER Michael Staehler <hamsterhase@gmail.com>

RUN apt-get update
RUN apt-get upgrade -y --force-yes
RUN apt-get install -y wget unzip dnsutils dos2unix

RUN wget -O /tmp/go-server.deb http://download.go.cd/gocd-deb/go-server-14.3.0-1186.deb

RUN dpkg -i /tmp/go-server.deb
RUN rm -f /tmp/go-server.deb

# CMD service go-server start
CMD /etc/init.d/go-server start && > /var/log/go-server/go-server.log && tail -F /var/log/go-server/go-server.log

EXPOSE 8153
EXPOSE 8154
