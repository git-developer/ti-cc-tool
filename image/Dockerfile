FROM python:3-alpine
ARG REPO_URL='cc2538-bsl[cc2538-bsl,intelhex] @ git+https://github.com/JelmerT/cc2538-bsl'
RUN apk add --no-cache file git && \
    printf %s 'sed -i "' "s/'--port', type=int,/'--port',/" '" cc2538-bsl.py' \
      | install -D /dev/stdin /usr/share/git-core/templates/hooks/post-checkout && \
    export PIP_ROOT_USER_ACTION=ignore && \
    pip3 install "${REPO_URL}" && \
    pip3 uninstall -y setuptools wheel pip && \
    apk del --no-cache -r git && \
    rm -r /root/.cache
RUN adduser -D user && addgroup user dialout
USER user
ADD run /usr/local/bin/
WORKDIR /tmp
ENTRYPOINT ["run"]
