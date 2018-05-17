FROM alpine
MAINTAINER kaku li

RUN apk update && apk add ca-certificates tzdata && rm -rf /var/cache/apk/* && mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2 && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone && mkdir -p /usr/share/filebeat

ADD filebeat-6.2.4-linux-x86_64/ /usr/share/filebeat
ADD filebeat_embed.yml /etc
RUN mv /etc/filebeat_embed.yml /etc/filebeat.yml
ADD filebeat /usr/share/filebeat


ENV ELASTIC_CONTAINER true
ENV PATH=/usr/share/filebeat:$PATH

COPY config /usr/share/filebeat

# Add entrypoint wrapper script
ADD docker-entrypoint /usr/local/bin

WORKDIR /usr/share/filebeat
RUN mkdir data logs && chmod +x /usr/local/bin/docker-entrypoint

ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]
CMD ["-e"]
