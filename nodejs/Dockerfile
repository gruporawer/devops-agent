FROM gruporawer/builder-base:v1.0.0

RUN ARCH= && uArch="$(uname -m)" \
  && case "${uArch##*-}" in \
    x86_64) ARCH='x64';; \
    aarch64) ARCH='arm64';; \
    *) echo "unsupported architecture"; exit 1 ;; \
  esac \
  && curl -sL "https://rpm.nodesource.com/setup_18.x" | bash - \
  && yum install -y nodejs gcc-c++ make bzip2 GConf2 gtk2 chromedriver chromium xorg-x11-server-Xvfb

RUN npm -g config set user root
RUN npm i -g watch-cli vsce typescript

# Yarn
RUN curl -f -L -o /tmp/yarn.tgz https://github.com/yarnpkg/yarn/releases/download/v${YARN_VERSION}/yarn-v${YARN_VERSION}.tar.gz && \
    sudo yum -y install yarn \
    yarn config set cache-folder /root/.yarn
