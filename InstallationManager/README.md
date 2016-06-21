# IBM Installation Manager
This image install IBM Installation Manager 1.6.2 (or another version) on a Docker container.
I use a RHEL 7.2 base.

## **`Dockerfiles`** links

* [`v0.1`](https://github.com/ingenieriainversa/Docker/blob/master/InstallationManager/Dockerfile) [(InstallationManager/Dockerfile)](https://github.com/ingenieriainversa/Docker/blob/master/InstallationManager/Dockerfile)

## How to use this image

Previously you need to download IBM Installation Manager (in this image v1.6.2) from the IBM official website, under license agreement. Unzip your downloaded software into `IM162_x64` folder. Also you need put the Dockerfile in the parent folder, like this:

```
- /my/folder/
         |
         |__IM162_x64
         |__Dockerfile
```

## How to build
To build this image run a command like the following:
`docker build -t rhel7.2-im .`

## How to run
Than you can run the container for the first time using:
`docker run -it --name InstallationManager --hostname rhel72 rhel7.2-im /bin/bash`

## License

```
 THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
 AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
 LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
 OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

 +------------------------------------------------------------------------+
 | Licensed Materials - Property of IBM                                   |
 | (C) Copyright IBM Corp. 2010, 2011.  All Rights Reserved.              |
 |                                                                        |
 | US Government Users Restricted Rights - Use, duplication or disclosure |
 | restricted by GSA ADP Schedule Contract with IBM Corp.                 |
 +------------------------------------------------------------------------+
```
