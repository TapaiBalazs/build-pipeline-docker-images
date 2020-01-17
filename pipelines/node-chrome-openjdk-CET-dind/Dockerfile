FROM cypress/browsers:node10.16.0-chrome77

# SETUP-LOCALE
RUN apt-get update \
    && apt-get install --assume-yes --no-install-recommends locales \
    && apt-get clean \
    && sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
    && sed -i -e 's/# hu_HU.UTF-8 UTF-8/hu_HU.UTF-8 UTF-8/' /etc/locale.gen \
    && locale-gen

ENV LANG="en_US.UTF-8" \
    LANGUAGE= \
    LC_CTYPE="en_US.UTF-8" \
    LC_NUMERIC="hu_HU.UTF-8" \
    LC_TIME="hu_HU.UTF-8" \
    LC_COLLATE="en_US.UTF-8" \
    LC_MONETARY="hu_HU.UTF-8" \
    LC_MESSAGES="en_US.UTF-8" \
    LC_PAPER="hu_HU.UTF-8" \
    LC_NAME="hu_HU.UTF-8" \
    LC_ADDRESS="hu_HU.UTF-8" \
    LC_TELEPHONE="hu_HU.UTF-8" \
    LC_MEASUREMENT="hu_HU.UTF-8" \
    LC_IDENTIFICATION="hu_HU.UTF-8" \
    LC_ALL=

# SETUP-TIMEZONE
RUN apt-get update \
    && apt-get install --assume-yes --no-install-recommends tzdata \
    && apt-get clean \
    && echo 'Europe/Budapest' > /etc/timezone && rm /etc/localtime \
    && ln -snf /usr/share/zoneinfo/'Europe/Budapest' /etc/localtime \
    && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update && apt-get install -y \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg2 \
        software-properties-common \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/debian \
        $(lsb_release -cs) \
        stable" \
    && apt-get update \
    && apt-get install -y \
        docker-ce

# Install OpenJDK-8
RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get clean;

# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME

RUN usermod -u 1002 node && groupmod -g 1002 node && gpasswd -a node docker
