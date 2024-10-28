FROM debian:12

RUN apt update && apt install -y net-tools procps most iproute2  iputils-ping dnsutils

RUN apt install -y bind9 dnsutils rsyslog bind9utils

RUN apt clean && rm -rf /var/lib/apt/lists/*

COPY entrypoint.sh /entrypoint.sh

RUN sed 's/OPTIONS=.*/OPTIONS="-u bind -4"/' /etc/default/named

RUN mkdir /var/log/bind && chown bind:bind /var/log/bind

RUN chmod +x /entrypoint.sh
ENTRYPOINT ["./entrypoint.sh"]