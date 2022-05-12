FROM postgres:12.10

# Use our local cache
#RUN echo 'Acquire::http { Proxy "http://apt-cacher:9999"; };' >> /etc/apt/apt.conf.d/01proxy

ENV DUMPFILE="gnuhealth-40-demo.sql.gz"
ENV SQLFILE="health301.sql"

#VOLUME /var/lib/postgresql
RUN apt-get update && apt-get install -y --no-install-recommends \
	gzip curl ca-certificates tar \
	&& rm -rf /var/lib/apt/lists/* \
	&& curl -o /$DUMPFILE -SL "http://health.gnu.org/downloads/postgres_dumps/$DUMPFILE" \	
	&& gzip -d $DUMPFILE 
COPY /home/analista/Docker-GnuHealth/postgres/$SQLFILE /
COPY /home/analista/Docker-GnuHealth/postgres/health-40-demo.sql.gz /
	#tar -xvf $DUMPFILE $SQLFILE \
RUN gzip -c $SQLFILE > demo.sql.gz \
	&& rm $DUMPFILE \
	&& apt-get purge -y --auto-remove curl ca-certificates

COPY gnuhealth.sh /docker-entrypoint-initdb.d/
