FROM debian:stretch

RUN dpkg --add-architecture i386 \
 && echo 'locales locales/locales_to_be_generated multiselect C.UTF-8 UTF-8, en_US.UTF-8 UTF-8 ' | debconf-set-selections \
 && echo 'locales locales/default_environment_locale select en_US.UTF-8' | debconf-set-selections \
 && apt-get update \
 && DEBIAN_FRONTEND=noninteractive apt-get dist-upgrade -y \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y devscripts locales \
 && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
 abootimg \
 autoconf \
 automake \
 bc \
 bison \
 build-essential \
 ccache \
 curl \
 debhelper \
 debian-archive-keyring \
 debian-keyring \
 device-tree-compiler \
 doxygen \
 fakeroot \
 flex \
 gcc \
 gdisk \
 git \
 kernel-wedge \
 kpartx \
 lava-tool \
 libstdc++6:i386 \
 libtool \
 lsb-release \
 openjdk-8-jdk \
 openssh-server \
 python-requests \
 qemu-user-static \
 sudo \
 time \
 u-boot-tools \
 uuid-dev \
 wget \
 zip \
 zlib1g:i386 \
 zsync \
 && apt-get clean \
 && rm -rf \
 /var/lib/apt/lists/* \
 /tmp/* \
 /var/tmp/*

RUN useradd -m buildslave \
 && echo 'buildslave ALL = NOPASSWD: ALL' > /etc/sudoers.d/jenkins \
 && chmod 440 /etc/sudoers.d/jenkins \
 && mkdir -p /var/run/sshd /home/buildslave/bin ;\
 apt clean ;\
 rm -rf /var/lib/apt/lists/*

EXPOSE 22
COPY entrypoint.sh /root/
ENTRYPOINT ["/root/entrypoint.sh"]
