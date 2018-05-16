FROM centos:7
MAINTAINER Elastic Docker Team <docker@elastic.co>

RUN yum update -y && yum install -y curl && yum clean all

ADD filebeat-6.2.4-linux-x86_64/ /usr/share/filebeat

ADD filebeat /usr/share/filebeat


ENV ELASTIC_CONTAINER true
ENV PATH=/usr/share/filebeat:$PATH

COPY config /usr/share/filebeat

# Add entrypoint wrapper script
ADD docker-entrypoint /usr/local/bin

WORKDIR /usr/share/filebeat
RUN mkdir data logs & chmod +x /usr/local/bin/docker-entrypoint

ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]
CMD ["-e"]
