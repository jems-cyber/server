#modified dockerfile from
#https://github.com/serfriz/caddy-custom-builds/blob/main/caddy-duckdns-crowdsec/Dockerfile

ARG CADDY_VERSION=2
#change this to the latest version
#better than automatic for security 

# removed "alpine" so it defaults to debian
# (easier to debug because tools are pre-installed)
FROM caddy:${CADDY_VERSION}-builder AS builder

RUN xcaddy build \
    --with github.com/mholt/caddy-l4 \
    --with github.com/caddyserver/transform-encoder \
    --with github.com/hslatman/caddy-crowdsec-bouncer/http@main \
    --with github.com/hslatman/caddy-crowdsec-bouncer/layer4@main

#removed "-alpine" here too
FROM caddy:${CADDY_VERSION} AS caddy

WORKDIR /

COPY --from=builder /usr/bin/caddy /usr/bin/caddy
