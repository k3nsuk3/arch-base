## -*- docker-image-name: "k3nsuk3/arch-base" -*-
FROM archlinuxjp/archlinux:latest
MAINTAINER Kensuke Kousaka <k@k3n.link>

RUN pacman -Syy --noconfirm

# Add normal user who can escalate to root without a password
COPY patches/sudoers.patch /tmp/sudoers.patch
RUN pacman -Syu --noconfirm base-devel ; \
  patch -u /etc/sudoers < /tmp/sudoers.patch && rm -f /tmp/sudoers.patch && \
  chown root:root /etc/sudoers && chmod 440 /etc/sudoers && \
  useradd -m -d /home/user -s /bin/bash -G wheel user

USER root

RUN pacman -Scc --noconfirm > /dev/null
ONBUILD RUN pacman -Syu --noconfirm &> /dev/null
