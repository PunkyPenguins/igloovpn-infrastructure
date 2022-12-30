ARG DEBIAN_VERSION=11.6

FROM debian:$DEBIAN_VERSION

ARG STRONGSWAN_VERSION=5.9.8

RUN apt-get -y update
RUN apt-get -y upgrade
RUN apt-get -y install curl bzip2 gcc make libssl-dev openssl

WORKDIR build

RUN curl https://download.strongswan.org/strongswan-${STRONGSWAN_VERSION}.tar.bz2 --output strongswan-${STRONGSWAN_VERSION}.tar.bz2 && \
    curl https://download.strongswan.org/strongswan-${STRONGSWAN_VERSION}.tar.bz2.md5 --output strongswan-${STRONGSWAN_VERSION}.tar.bz2.md5 && \
    md5sum -c strongswan-${STRONGSWAN_VERSION}.tar.bz2.md5  && \
    tar --strip-components=1 -xjf strongswan-${STRONGSWAN_VERSION}.tar.bz2 && \
    rm strongswan-${STRONGSWAN_VERSION}.tar.bz2 strongswan-${STRONGSWAN_VERSION}.tar.bz2.md5

RUN ./configure \
    --disable-shared \
    --enable-static \
    --enable-monolithic \
    --prefix=/usr \
    --sysconfdir=/etc \
    --enable-aesni \
    --enable-chapoly \
    --enable-ha \
    --enable-dhcp \
    --enable-eap-dynamic \
    --enable-eap-identity \
    --enable-eap-md5 \
    --enable-eap-mschapv2 \
    --enable-eap-tls \
    --enable-farp \
    --enable-files \
    --enable-gcm \
    --enable-md4 \
    --enable-newhope \
    --enable-ntru \
    --enable-openssl \
    --enable-sha3 \
    --enable-shared \
    --enable-vici \
    --disable-aes \
    --disable-des \
    --disable-gmp \
    --disable-hmac \
    --disable-ikev1 \
    --disable-md5 \
    --disable-rc2 \
    --disable-sha1 \
    --disable-sha2 \
    --disable-static \
    --disable-mysql \
    --disable-sql

RUN make && make install

EXPOSE 500/udp \
       4500/udp

ENTRYPOINT ["/usr/sbin/ipsec"]
CMD ["start", "--nofork"]