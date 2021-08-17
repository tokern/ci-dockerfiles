FROM circleci/python:3.8.11-buster

WORKDIR /tmp

RUN set -ex \
    && GOURL="https://dl.google.com/go/go1.17.linux-amd64.tar.gz" \
    && echo GO URL: $GOURL \
    && curl --silent --show-error --location --fail --retry 3 --output /tmp/go.tgz "${GOURL}" \
    && ls -lha /tmp/go.tgz \
    && tar -xz -C /tmp -f /tmp/go.tgz \
    && sudo mv go /usr/local \
    && rm -rf /tmp/go /tmp/go.tgz

USER circleci
ENV GOROOT=/usr/local/go
ENV GOPATH=/home/circleci/go

ENV PATH /home/circleci/.local/bin:/home/circleci/bin:${GOROOT}/bin:${GOPATH}/bin:${PATH}

RUN go get github.com/aktau/github-release
RUN go get github.com/git-chglog/git-chglog/cmd/git-chglog

CMD ["/bin/sh"]
