FROM royalsarkis/liferay_arm64:zulu-openjdk11-arm64

ARG LABEL_BUILD_DATE
ARG LABEL_NAME
ARG LABEL_VCS_REF
ARG LABEL_VCS_URL
ARG LABEL_VERSION

RUN apt-get -q update && \
	apt-get -yq install gnupg curl && \
	apt-key adv \
  	--keyserver hkp://keyserver.ubuntu.com:80 \
  	--recv-keys 0xB1998361219BD9C9 && \
	curl -O https://cdn.azul.com/zulu/bin/zulu-repo_1.0.0-3_all.deb && \
	apt-get install ./zulu-repo_1.0.0-3_all.deb 

RUN apt-get update && \
	apt-get install -y bash curl ffmpeg ghostscript gifsicle imagemagick jattach libnss3 libtcnative-1 telnet tini tree ttf-dejavu unzip zulu8-jdk && \
	apt-get upgrade -y && \
	apt-get clean

COPY scripts/* /usr/local/bin/
RUN chmod u+x /usr/local/bin/*

RUN adduser --disabled-password --home /home/liferay liferay --uid 1000 && \
	addgroup liferay liferay && \
	usermod -g 1000 liferay

COPY --chown=liferay:liferay home/.bashrc /home/liferay/

ENV JAVA_VERSION=zulu8-ca-arm64


LABEL org.label-schema.build-date="${LABEL_BUILD_DATE}"
LABEL org.label-schema.name="${LABEL_NAME}"
LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.vcs-ref="${LABEL_VCS_REF}"
LABEL org.label-schema.vcs-url="${LABEL_VCS_URL}"
LABEL org.label-schema.vendor="Liferay, Inc."
LABEL org.label-schema.version="${LABEL_VERSION}"