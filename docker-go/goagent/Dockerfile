FROM dockerfile/java
MAINTAINER Michael Staehler <hamsterhase@gmail.com>

RUN wget -O /tmp/go-agent.deb http://download.go.cd/gocd-deb/go-agent-14.3.0-1186.deb
RUN dpkg -i /tmp/go-agent.deb
RUN rm -f /tmp/go-agent.deb

ENV SERVER_ID $(dig @172.17.42.1 +short dockergo_goserver_1.dockergo_goserver.dev.docker)

RUN echo GO_SERVER=$SERVER_ID >> /etc/default/go-agent
RUN sed -i 's/DAEMON=Y/DAEMON=N/g' /etc/default/go-agent

# make sure that init.d script passes through environment variables
# RUN sed -i 's/su -/su -p/' /etc/init.d/go-agent

# CMD su go -c '/etc/init.d/go-agent start'

# RUN sed -r -i "s/^(GO_SERVER)=(.*)/\1=\8153/g" /etc/default/go-agent

VOLUME ["/var/lib/go-agent"]

CMD /usr/lib/jvm/java-7-openjdk-amd64/bin/java -jar /usr/share/go-agent/agent-bootstrapper.jar $SERVER_ID 8153
