FROM buildpack-deps:jessie-curl

RUN wget -q https://repos.influxdata.com/influxdb.key && \
    gpg --import influxdb.key && \
    rm -f influxdb.key

ENV INFLUXDB_VERSION 0.12.0
RUN wget -q https://s3.amazonaws.com/influxdb/influxdb_$INFLUXDB_VERSION-1_amd64.deb.asc && \
    wget -q https://s3.amazonaws.com/influxdb/influxdb_$INFLUXDB_VERSION-1_amd64.deb && \
    gpg --verify influxdb_$INFLUXDB_VERSION-1_amd64.deb.asc influxdb_$INFLUXDB_VERSION-1_amd64.deb && \
    dpkg -i influxdb_$INFLUXDB_VERSION-1_amd64.deb && \
    rm -f influxdb_$INFLUXDB_VERSION-1_amd64.deb*

EXPOSE 8083 8086

ENV INFLUXDB_META_DIR=/var/lib/influxdb/meta \
    INFLUXDB_DATA_DIR=/var/lib/influxdb/data \
    INFLUXDB_DATA_WAL_DIR=/var/lib/influxdb/wal
VOLUME /var/lib/influxdb

COPY entrypoint.sh /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["influxd"]