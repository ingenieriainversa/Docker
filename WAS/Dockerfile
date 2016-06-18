# To build this image run a command like the following:
# docker build -t rhel7.2-was .
#
# Than you can run the container for the first time using:
# docker run -it --name WebSphere8.5 --hostname rhel-javi -p 9060:9060 -p 9080:9080 rhel7.2-was /bin/bash
# the command above creates the image with the name WebSphere8.5, you can change it to whatever you want.
#
# Once you've runned the container and it's already created, use start instead of run.(replace the $CONTAINER_NAME) with
# the name you have picked during the run command above.
# docker start $CONTAINER_NAME /bin/bash
#
# and if needed to attach to the running container
# docker attach $CONTAINER_NAME

FROM rhel7.2-im

MAINTAINER Javier Dominguez Gomez "jdg@member.fsf.org"

ENV USER was
ENV WAS_HOME /opt/IBM/WebSphere8.5
ENV WAS_SW_BASE WAS
ENV IM_HOME /opt/IBM/InstallationManager/eclipse

RUN groupadd -r $USER && useradd -r -g $USER $USER

COPY $WAS_SW_BASE /tmp/$WAS_SW_BASE
COPY responsefile.rsp /tmp/responsefile.rsp

RUN cd $IM_HOME && ./IBMIM --launcher.ini silent-install.ini -acceptLicense -input /tmp/responsefile.rsp

RUN chmod -R 750 $WAS_HOME && chown -R $USER:$USER $WAS_HOME && rm -fr /tmp/$WAS_SW_BASE /tmp/responsefile.rsp

RUN /opt/IBM/WebSphere8.5/AppServer/bin/manageprofiles.sh -create -templatePath /opt/IBM/WebSphere8.5/AppServer/profileTemplates/management

EXPOSE 9080 9060
