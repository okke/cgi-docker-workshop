FROM nlcgi/base

RUN apt-get install -y redis-server

EXPOSE 6379

ADD startup.sh /tmp/
RUN tr -d '\r' < /tmp/startup.sh > .tmp
RUN mv -f .tmp /tmp/startup.sh
RUN chmod +x /tmp/startup.sh
ENTRYPOINT exec /tmp/startup.sh
