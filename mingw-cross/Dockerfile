FROM base/archlinux:2018.05.01
MAINTAINER Dirk Vanden Boer <dirk.vdb@gmail.com>
RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm git cmake gcc clang flex make patch ninja base-devel pkgconfig openssh unzip help2man
RUN git clone https://github.com/crosstool-ng/crosstool-ng.git
RUN cd crosstool-ng && ./bootstrap && ./configure && make install
RUN useradd -ms /bin/bash builder

USER builder
RUN mkdir -p /home/builder/mingw
COPY x86_64-w64-mingw32.config /home/builder/mingw/.config
WORKDIR /home/builder/mingw
RUN ct-ng build
WORKDIR /home/builder
RUN rm -rf mingw
RUN  echo "export PATH=/home/builder/x-tools/x86_64-w64-mingw32/bin:$PATH" >> .bashrc

