# WebSphere Application Server ND 8.5.5.0 install on a docker container.
# By Javier Dominguez Gomez - jdg@member.fsf.org
# The base image used already contains Installation Manager 1.6.2 installed.
# WebSphere Application Server ND can be downloaded from IBM web site:
# http://www.ibm.com/developerworks/downloads/ws/was/
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

# You may need to download the software previously and put it into WAS folder.
ENV WAS_SW_BASE WAS

# The path that WAS will be installed
ENV WAS_HOME /opt/IBM/WebSphere8.5

# The path where Installation Manager was previously installed.
ENV IM_HOME /opt/IBM/InstallationManager/eclipse

# Define the user that will be creted.
ENV USER was

# Set the hostname for WAS
ENV HOSTNAME c-javi

# Create WAS group and user.
RUN groupadd -r $USER && useradd -r -g $USER $USER

# Copy WAS Software base files and responsefile.xml to docker image.
COPY $WAS_SW_BASE /tmp/$WAS_SW_BASE
COPY responsefile.xml /tmp/responsefile.xml

# Execute the installation manager instruction to use this response file and the
# was repo we've created and execute the installation.
RUN cd $IM_HOME && ./IBMIM --launcher.ini silent-install.ini -acceptLicense -input /tmp/responsefile.xml

# When the installation is done we change the install path permissions and delete
# the repository so the image doesn't get tooooo big (it's big anyway).
RUN chmod -R 750 $WAS_HOME && chown -R $USER:$USER $WAS_HOME && rm -fr /tmp/$WAS_SW_BASE /tmp/responsefile.xml

# Create and federate a DMGR and AppSrv profiles (using all default) in a cell.
RUN $WAS_HOME/AppServer/bin/manageprofiles.sh -create -profileName Dmgr_$HOSTNAME -profilePath $WAS_HOME/AppServer/profiles/Dmgr_$HOSTNAME -templatePath $WAS_HOME/AppServer/profileTemplates/management -nodeName Dmgr_${HOSTNAME}_node -cellName Cell_$HOSTNAME -hostName $HOSTNAME -enableAdminSecurity true -adminUserName admin -adminPassword 1234
RUN $WAS_HOME/AppServer/bin/manageprofiles.sh -create -profileName AppSrv_$HOSTNAME -profilePath $WAS_HOME/AppServer/profiles/AppSrv_$HOSTNAME -templatePath $RUTA_WAS/AppServer/profileTemplates/managed -nodeName AppSrv_${HOSTNAME}_node -hostName $HOSTNAME
RUN $WAS_HOME/AppServer/profiles/AppSrv_$HOSTNAME/bin/addNode.sh $HOSTNAME 8879 -username admin -password 1234

# Let's expose at least HTTP and DMGR ports for this profile.
EXPOSE 9080 9060
