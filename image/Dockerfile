FROM python:3-alpine
ARG REPO_URL='cc2538-bsl[default,intelhex] @ git+https://github.com/JelmerT/cc2538-bsl'
# sed is used as post-checkout hook to fix `setup.py`, see https://github.com/JelmerT/cc2538-bsl/pull/143
RUN apk add --no-cache file git && \
    printf %s 'sed -i "' "s/'':/'default':/" '" setup.py' \
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
