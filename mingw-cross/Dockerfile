FROM archlinux/base:latest
LABEL Author="Dirk Vanden Boer"
LABEL maintainer="dirk.vdb@gmail.com"
RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm git cmake gcc flex make patch ninja base-devel pkgconfig openssh unzip help2man
RUN git clone --branch crosstool-ng-1.24.0 https://github.com/crosstool-ng/crosstool-ng.git
RUN cd crosstool-ng && ./bootstrap && ./configure && make install
RUN useradd -ms /bin/bash builder

USER builder
RUN mkdir -p /home/builder/mingw
WORKDIR /home/builder/mingw
RUN ct-ng x86_64-w64-mingw32
RUN echo "CT_CC_GCC_LIBGOMP=y" >> .config
RUN echo "CT_CC_GCC_LIBQUADMATH=y" >> .config
RUN ct-ng build && cd .. && rm -rf mingw
WORKDIR /home/builder
RUN  echo "export PATH=/home/builder/x-tools/x86_64-w64-mingw32/bin:$PATH" >> .bashrc

