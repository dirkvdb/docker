FROM archlinux/base:latest
LABEL Author="Dirk Vanden Boer"
LABEL maintainer="dirk.vdb@gmail.com"
RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm git cmake gcc flex make patch ninja base-devel pkgconfig openssh unzip help2man python3
RUN git clone --branch crosstool-ng-1.24.0 https://github.com/crosstool-ng/crosstool-ng.git
RUN cd crosstool-ng && ./bootstrap && ./configure && make install
RUN useradd -ms /bin/bash builder

USER builder
RUN mkdir -p /home/builder/musl
WORKDIR /home/builder/musl
RUN ct-ng x86_64-multilib-linux-musl
RUN echo "CT_CC_GCC_LIBGOMP=y" >> .config
RUN echo "CT_CC_GCC_LIBQUADMATH=y" >> .config
RUN sed -i 's/CT_DEBUG_DUMA=y/CT_DEBUG_DUMA=n/g' .config
RUN cat .config
RUN ct-ng build && cd .. && rm -rf musl
WORKDIR /home/builder
RUN  echo "export PATH=/home/builder/x-tools/x86_64-multilib-linux-musl/bin:$PATH" >> .bashrc

