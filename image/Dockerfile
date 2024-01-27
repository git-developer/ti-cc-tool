FROM alpine
ARG REPO_URL=git+https://github.com/JelmerT/cc2538-bsl#egg=cc2538-bsl[default,intelhex]
# sed is used as post-checkout hook to fix `setup.py`, see https://github.com/JelmerT/cc2538-bsl/pull/143
RUN apk add --no-cache python3 file pipx git && \
    printf %s 'sed -i "' "s/'':/'default':/" '" setup.py' | install /dev/stdin /usr/share/git-core/templates/hooks/post-checkout && \
    PIPX_HOME=/opt/pipx PIPX_BIN_DIR=/usr/local/bin pipx install "${REPO_URL}" && \
    apk del --no-cache git pipx
ADD run /usr/local/bin/
WORKDIR /tmp
ENTRYPOINT ["run"]
