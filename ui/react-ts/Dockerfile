FROM eleidan/node:14.15.4-ubuntu-20.04

USER root

### Browser tests need a browser
ARG CHROME_FILE="google-chrome-stable_current_amd64.deb"
RUN wget https://dl.google.com/linux/direct/${CHROME_FILE} \
    && apt-get update \
    && apt install -y ./${CHROME_FILE} \
    && rm ${CHROME_FILE}

### Adapt container user for the host UID and GID
ARG HOST_UID=1000
ARG HOST_GID=1000
RUN usermod -u ${HOST_UID} phantom
RUN groupmod -g ${HOST_GID} phantom
RUN chown -R phantom:phantom ${HOME}

### System Update
RUN apt-get update && apt-get upgrade -y

USER phantom

### Acess peoject binaries
ENV PATH="${PATH}:${HOME}/node_modules/.bin"

WORKDIR ${HOME}/app

