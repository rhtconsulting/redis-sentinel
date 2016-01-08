FROM rhel7:latest
RUN yum -y update
RUN yum -y install make gcc cc tar python

#FROM redis:2.8
#RUN yum install -yy -q python
RUN \
  cd /tmp && \
  curl -O http://download.redis.io/redis-stable.tar.gz && \
  tar xvzf redis-stable.tar.gz && \
  cd redis-stable && \
  cd deps && \
  make hiredis jemalloc linenoise lua && \
  cd .. && \
  make && \
  make install && \
  cp -f src/redis-sentinel /usr/local/bin && \
  mkdir -p /redis-master && \
  mkdir -p /redis-slave && \
#  mkdir -p /etc/redis && \
#  cp -f *.conf /etc/redis && \
  rm -rf /tmp/redis-stable*


COPY redis-master.conf /redis-master/redis.conf
COPY redis-slave.conf /redis-slave/redis.conf
COPY run.sh /run.sh

CMD [ "/run.sh" ]
ENTRYPOINT [ "sh", "-c" ]
