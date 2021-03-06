FROM phalconphp/bootstrap:ubuntu-18.04

LABEL description="Slimmed-down base image to use for production with Ubuntu 18.04 and supervisord" \
    maintainer="Serghei Iakovlev <serghei@phalconphp.com>" \
    vendor=Phalcon \
    name="com.phalconphp.images.base.ubuntu-18.04"

RUN apt clean -y \
    && apt update -y \
    && apt upgrade -y \
    && apt install --no-install-recommends -yq \
        cron \
        curl \
        dnsutils \
        git \
        gnupg \
        iproute2 \
        jq \
        less \
        logrotate \
        lsb-release \
        net-tools \
        sudo \
        supervisor \
        swig \
        tmpreaper \
        unzip \
        vim \
        wget \
    && echo '%adm ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers \
    && mkdir -p /var/log/supervisor \
    && sed -i "s/^[\s]*su root syslog/# su root syslog/g" /etc/logrotate.conf \
    && apt autoremove -y \
    && apt clean -y \
    && rm -rf /tmp/* /var/tmp/* \
    && find /var/cache/apt/archives /var/lib/apt/lists -not -name lock -type f -delete \
    && find /var/cache -type f -delete \
    && find /var/log -type f | while read f; do echo -n '' > ${f}; done

ADD configs /

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
