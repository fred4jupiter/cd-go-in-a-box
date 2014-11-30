FROM dockerfile/java
MAINTAINER Michael Staehler <hamsterhase@gmail.com>

RUN apt-get update
RUN apt-get upgrade -y --force-yes
RUN apt-get install -y wget unzip dnsutils dos2unix

RUN wget -O /tmp/go-agent.deb http://download.go.cd/gocd-deb/go-agent-14.3.0-1186.deb

RUN dpkg -i /tmp/go-agent.deb
RUN rm /tmp/go-agent.deb

RUN sed -i 's/GO_SERVER=127.0.0.1/GO_SERVER=`dig @172.17.42.1 +short vagrant_goserver.dev.docker`/g' /etc/default/go-agent
RUN sed -i 's/DAEMON=Y/DAEMON=N/g' /etc/default/go-agent

CMD service go-agent start
