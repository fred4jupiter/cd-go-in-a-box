FROM dockerfile/java
MAINTAINER Michael Staehler <hamsterhase@gmail.com>

RUN wget -O /tmp/go-agent.deb http://download.go.cd/gocd-deb/go-agent-14.3.0-1186.deb
RUN dpkg -i /tmp/go-agent.deb
RUN rm -f /tmp/go-agent.deb

RUN sed -i 's/GO_SERVER=127.0.0.1/GO_SERVER=`dig +short dockergo_goserver_1.dockergo_goserver.dev.docker`/g' /etc/default/go-agent
RUN sed -i 's/DAEMON=Y/DAEMON=N/g' /etc/default/go-agent

# make sure that init.d script passes through environment variables
RUN sed -i 's/su -/su -p/' /etc/init.d/go-agent

CMD su go -c '/etc/init.d/go-agent start'