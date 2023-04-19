FROM fedora:36
MAINTAINER Giulio Benetti <giulio.benetti@benettiengineering.com>

LABEL maintainer="Giulio Benetti <giulio.benetti@benettiengineering.com>" \
description="Container with everything needed to run Buildroot"

# Install dependencies
RUN dnf update -y
RUN dnf install -y \
  bc \
  bison \
  bzip2 \
  cmake \
  cpio \
  dialog \
  expect \
  file \
  flex \
  gcc \
  gcc-c++ \
  git \
  make \
  mc \
  nano \
  ncurses-devel \
  patch \
  perl-Data-Dumper \
  perl-English \
  perl-FindBin \
  perl-ExtUtils-MakeMaker \
  perl-Thread-Queue \
  rsync \
  sudo \
  svn \
  unzip \
  wget \
  which \
  xz

# 32bit binaries
RUN set -e; \
  dnf install -y \
  glibc-devel.i686 \
  libgcc.i686 \
  libstdc++-devel.i686 \
  ncurses-devel.i686 \
  zlib.i686 \
  glibc.i686

RUN set -e; \
  dnf install -y python3-pip; \
  pip3 install -U pip --prefix=/usr; \
  pip3 install \
  nose2==0.9.2 \
  pexpect==4.8.0 \
  spdx_lookup==0.3.3;

RUN set -e; \
  useradd -ms /bin/bash br-user; \
  echo "alias ls='ls --color=auto'" >> /home/br-user/.bashrc; \
  echo "PS1='\u@\H [\w]$ '" >> /home/br-user/.bashrc;

RUN set -e; \
  chown -R br-user:br-user /home/br-user; \
  echo "alias ls='ls --color=auto'" >> /root/.bashrc; \
  echo "PS1='\u@\H [\w]$ '" >> /root/.bashrc

RUN set -e; \
  echo "LC_ALL=en_US.UTF-8" >> /etc/environment \
  echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
  echo "LANG=en_US.UTF-8" > /etc/locale.conf \
  locale-gen en_US.UTF-8

COPY brmake /usr/bin

USER br-user
ENV HOME /home/br-user
#ENV LC_ALL en_US.UTF-8

CMD ["/bin/bash"]
