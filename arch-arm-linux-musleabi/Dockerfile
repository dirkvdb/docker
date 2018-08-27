FROM base/archlinux:2018.08.01
RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm gcc flex bison
RUN pacman -S --noconfirm git cmake make patch ninja autoconf automake libtool pkgconfig wget texinfo vim openssh ruby-rake

# Install musl-cross
RUN mkdir /build &&                                                 \
    cd /build &&                                                    \
    git clone https://github.com/GregorR/musl-cross.git &&          \
    cd musl-cross &&                                                \
    echo 'ARCH=arm'                                 >> config.sh && \
    echo 'TRIPLE=arm-linux-musleabi'                >> config.sh && \
    echo 'GCC_BOOTSTRAP_CONFFLAGS="--with-arch=armv5 --with-float=soft"' >> config.sh && \
    echo 'GCC_CONFFLAGS="--with-arch=armv5 --with-float=soft"' >> config.sh && \
    ./build.sh &&                                                   \
    cd / &&                                                         \
    rm -rf /tmp/* /var/tmp/* /build

ENV PATH $PATH:/opt/cross/arm-linux-musleabi/bin
CMD /bin/bash

