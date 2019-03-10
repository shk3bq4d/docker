FROM docker:stable

COPY root.ly.lan.crt /usr/local/share/ca-certificates/root.ly.lan.crt
RUN true  \
	&& apk add -U \
		bash \
		ca-certificates \
		git \
		jq \
	&& rm -rf /var/cache/apk/* \
	&& update-ca-certificates \
	&& true
