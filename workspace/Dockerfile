FROM laradock/workspace:2.2-7.2

RUN DEBIAN_FRONTEND=noninteractive
RUN locale-gen en_US.UTF-8

ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LC_CTYPE=UTF-8
ENV LANG=en_US.UTF-8
ENV TERM xterm

#####################################
# Other Software
#####################################
RUN apt-get update && apt-get install -y \
    python \
    ruby \
    ruby-dev \
    libcurl4-openssl-dev \
    libedit-dev \
    libssl-dev \
    libxml2-dev \
    git \
    curl \
    vim

# Install Compass GEM for SASS compilation.
RUN gem install compass

#####################################
# Non-Root User
#####################################
ARG PGID=1000
ARG PUID=1000

RUN groupadd -g $PGID nuswhispers && \
    useradd -u $PUID -g nuswhispers -m nuswhispers

#####################################
# Timezone
#####################################
ARG TZ=UTC
ENV TZ=${TZ}
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

#####################################
# Composer
#####################################
RUN mkdir /home/nuswhispers/.composer && \
    chown -R nuswhispers:nuswhispers /home/nuswhispers/.composer

USER nuswhispers

# Export bin folders to PATH.
RUN echo "" >> ~/.bashrc && \
    echo "export PATH=${PATH}:/var/www/nuswhispers/vendor/bin" >> ~/.bashrc

#####################################
# xDebug
#####################################
USER root

RUN apt-get update && \
    apt-get install -y php7.2-xdebug && \
    sed -i 's/^;//g' /etc/php/7.2/cli/conf.d/20-xdebug.ini && \
    echo "alias phpunit='php -dzend_extension=xdebug.so /var/www/vendor/bin/phpunit'" >> ~/.bashrc

COPY xdebug.ini /etc/php/7.2/cli/conf.d/xdebug.ini

#####################################
# SSH
#####################################
ADD insecure_id_rsa /tmp/id_rsa
ADD insecure_id_rsa.pub /tmp/id_rsa.pub

RUN rm -f /etc/service/sshd/down \
    && cat /tmp/id_rsa.pub >> /root/.ssh/authorized_keys \
    && cat /tmp/id_rsa.pub >> /root/.ssh/id_rsa.pub \
    && cat /tmp/id_rsa >> /root/.ssh/id_rsa \
    && rm -f /tmp/id_rsa* \
    && chmod 644 /root/.ssh/authorized_keys /root/.ssh/id_rsa.pub \
    && chmod 400 /root/.ssh/id_rsa

#####################################
# Node (nvm)
#####################################
USER nuswhispers

ARG NODE_VERSION=stable
ENV NODE_VERSION ${NODE_VERSION}

ENV NVM_DIR=/home/nuswhispers/.nvm
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.6/install.sh | bash && \
    . $NVM_DIR/nvm.sh && \
    nvm install ${NODE_VERSION} && \
    nvm use ${NODE_VERSION} && \
    nvm alias ${NODE_VERSION} && \
    npm install -g gulp bower

# Source NVM when loading bash since ~/.profile isn't loaded on non-login shell
RUN echo "" >> ~/.bashrc && \
    echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc && \
    echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> ~/.bashrc

USER root

RUN echo "" >> ~/.bashrc && \
    echo 'export NVM_DIR="/home/nuswhispers/.nvm"' >> ~/.bashrc && \
    echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm' >> ~/.bashrc


#####################################
# Final Touches
#####################################

# Clean up
USER root
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /var/www/nuswhispers
