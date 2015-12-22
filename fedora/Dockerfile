# fedora settings for compilation build 
From fedora:23
MAINTAINER Vincent Jardin <vj@6wind.com>

LABEL version="head"
LABEL description="Quagga smoke and compilation test."

RUN dnf -qy update
RUN dnf -qy install git dh-autoreconf readline-devel texinfo
RUN dnf -qy install quagga-devel

WORKDIR /home/q/src
RUN git clone git://git.sv.gnu.org/quagga.git

WORKDIR /home/q/src/quagga
RUN ./bootstrap.sh && \
    ./configure --prefix=/usr --enable-user=quagga --enable-group=quagga --enable-vty-group=quagga \
    --enable-multipath=16 --enable-werror \
    --enable-configfile-mask=0660 --enable-logfile-mask=0640 \
    --enable-vtysh --enable-rtadv --disable-static --enable-isisd \
    --enable-pimd \
    --sysconfdir=/etc/quagga --enable-exampledir=/etc/quagga/samples --localstatedir=/var/run/quagga \
    --libdir=/usr/lib64/quagga
RUN make
RUN make install

# Quagga ports for vtys
# EXPOSE 260X

# BGP port
# EXPOSE 

CMD bash
