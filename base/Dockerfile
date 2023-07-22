FROM ubuntu:23.10

# utils
RUN apt-get update && \
  apt-get install -y software-properties-common && \
  add-apt-repository ppa:git-core/ppa

# Install base dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    sudo \
    build-essential \
    ca-certificates \
    curl \
    git \
    fakeroot \
    clang \
    cmake \
    libsecret-1-dev \
    libnss3 \
    libgtk2.0-dev \
    libgtk-3-dev \
    libnotify-dev \
    libdbus-1-dev \
    libxrandr-dev \
    libxext-dev \
    libxss-dev \
    libgconf2-dev \
    libasound2-dev \
    libcap-dev \
    libcups2-dev \
    libxtst-dev \
    libcurl4-openssl-dev \
    libxkbfile-dev \
    curl \
    wget \
    xvfb \
    snapd \
    make \
    zip \
    unzip \
    bzip2 \
    openssl \
    zlib1g \
    zlib1g-dev \
    python3 \
    python3-pip \
    openjdk-8-jdk \
    autoconf \
    bison \
    perl \
    libssl-dev \
    libyaml-dev \
    libreadline6-dev \
    zlib1g-dev \
    libncurses5-dev \
    libffi-dev \
    libgmp-dev \
    libgdbm-dev \
    libdb-dev \
    gettext \
    # snapcraft \
    squashfs-tools \
    --no-install-recommends

RUN wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.9.5.tar.gz && \
    tar zxvf git-2.9.5.tar.gz --no-same-owner && \
    cd git-2.9.5 && \
    make configure && \
    ./configure prefix=/usr/local/git/ && \
    make && \
    make install && \
    mv /usr/local/git/bin/git /usr/bin/ && \
    cd ..&& \
    rm -rf git-2.9.5.tar.gz git-2.9.5 && \
    git version

# Set the locale(en_US.UTF-8)
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# USER jenkins
WORKDIR /home/jenkins

ENV SONAR_SCANNER_VERSION 3.3.0.1492

RUN curl -o sonar_scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-${SONAR_SCANNER_VERSION}-linux.zip && \
    unzip sonar_scanner.zip && rm sonar_scanner.zip \
    && rm -rf sonar-scanner-$SONAR_SCANNER_VERSION-linux/jre && \
    sed -i 's/use_embedded_jre=true/use_embedded_jre=false/g' /home/jenkins/sonar-scanner-$SONAR_SCANNER_VERSION-linux/bin/sonar-scanner && \
    mv /home/jenkins/sonar-scanner-$SONAR_SCANNER_VERSION-linux /usr/bin

ENV PATH $PATH:/usr/bin/sonar-scanner-$SONAR_SCANNER_VERSION-linux/bin

COPY ./ ./
RUN ./hack/install_utils.sh && rm -rf ./*

CMD ["docker","version"]
