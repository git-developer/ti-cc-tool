FROM alpine
ARG REPO_URL=git+https://github.com/JelmerT/cc2538-bsl
RUN apk add --no-cache python3 file py3-pip git && pip3 install pyserial intelhex $REPO_URL && apk del git py3-pip
ADD run /usr/local/bin/
WORKDIR /tmp
ENTRYPOINT ["run"]
