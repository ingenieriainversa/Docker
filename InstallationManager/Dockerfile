FROM rhel7.2:latest
MAINTAINER Javier Dominguez Gomez

RUN groupadd -r imanager && useradd -r -g imanager imanager

COPY BASE/IM162_x64 /tmp/IM162_x64

RUN cd /tmp/IM162_x64 && ./installc -log /opt/im_install.log -acceptLicense && rm -rf /tmp/*

RUN cd /opt && chown -R imanager:imanager IBM
