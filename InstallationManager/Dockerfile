FROM rhel7.2:latest

MAINTAINER Javier Dominguez Gomez "jdg@member.fsf.org"

ENV USER imanager
ENV BIN_FILES_DIR /software/IM162_x64
ENV IM_HOME /opt/IBM/InstallationManager

RUN groupadd -r $USER && useradd -r -g $USER $USER

COPY $BIN_FILES_DIR /tmp/$BIN_FILES_DIR

RUN cd /tmp/$BIN_FILES_DIR && \
./install --launcher.ini silent-install.ini -acceptLicense -dataLocation /home/$USER/dataLocation -installationDirectory $IM_HOME && \
rm -rf /tmp/$BIN_FILES_DIR

RUN chown -R $USER:$USER $IM_HOME
