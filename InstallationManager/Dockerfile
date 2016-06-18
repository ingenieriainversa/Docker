# IBM Installation Manager 1.6.2 install on a docker container.
# By Javier Dominguez Gomez - jdg@member.fsf.org
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
#
# +------------------------------------------------------------------------+
# | Licensed Materials - Property of IBM                                   |
# | (C) Copyright IBM Corp. 2010, 2011.  All Rights Reserved.              |
# |                                                                        |
# | US Government Users Restricted Rights - Use, duplication or disclosure |
# | restricted by GSA ADP Schedule Contract with IBM Corp.                 |
# +------------------------------------------------------------------------+
#
# To build this image run a command like the following:
# docker build -t rhel7.2-im .
#
# Than you can run the container for the first time using:
# docker run -it --name InstallationManager --hostname rhel-javi rhel7.2-im /bin/bash

FROM rhel7.2:latest

MAINTAINER Javier Dominguez Gomez "jdg@member.fsf.org"

ENV USER imanager
ENV BIN_FILES_DIR IM162_x64
ENV IM_HOME /opt/IBM/InstallationManager

RUN groupadd -r $USER && useradd -r -g $USER $USER

COPY $BIN_FILES_DIR /tmp/$BIN_FILES_DIR

RUN cd /tmp/$BIN_FILES_DIR && \
./install --launcher.ini silent-install.ini -acceptLicense -dataLocation /home/$USER/dataLocation -installationDirectory $IM_HOME && \
rm -rf /tmp/$BIN_FILES_DIR

RUN chown -R $USER:$USER $IM_HOME
