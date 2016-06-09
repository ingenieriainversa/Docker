FROM rhel7.2-im:latest
 
MAINTAINER Javier Dominguez Gomez
 
ENV USER was
ENV WAS_HOME /opt/IBM/WebSphere
ENV WAS_SW_BASE /software/WAS
ENV WAS_PLG_SW_BASE /software/WAS_SUPPLEMENTS
ENV USER_HOME /home/$USER
ENV IM_HOME /opt/IBM/InstallationManager/eclipse
 
RUN groupadd was && useradd -c "WebSphere user" -d $USER_HOME -m -s /bin/bash -g $USER -u was && chmod 750 $USER_HOME
 
RUN cd $IM_HOME && ./IBMIM --launcher.ini silent-install.ini -acceptLicense -input responsefile.rsp
 
RUN chmod -R 750 $WAS_HOME && chown -R $USER:$USER $WAS_HOME
