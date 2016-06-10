FROM local/rhel7.2-im:v1

MAINTAINER Javier Dominguez Gomez "jdg@member.fsf.org"

ENV USER was
ENV WAS_HOME /opt/IBM/WebSphere
ENV WAS_SW_BASE WAS
ENV WAS_PLG_SW_BASE WAS_SUPPLEMENTS
ENV USER_HOME /home/$USER
ENV IM_HOME /opt/IBM/InstallationManager/eclipse

RUN groupadd -r $USER && useradd -r -g $USER $USER

COPY $WAS_SW_BASE /tmp/$WAS_SW_BASE
COPY $WAS_PLG_SW_BASE /tmp/$WAS_PLG_SW_BASE
COPY responsefile.rsp /tmp/responsefile.rsp

RUN cd $IM_HOME && ./IBMIM --launcher.ini silent-install.ini -acceptLicense -input /tmp/responsefile.rsp && rm -fr /tmp/*

RUN chmod -R 750 $WAS_HOME && chown -R $USER:$USER $WAS_HOME
