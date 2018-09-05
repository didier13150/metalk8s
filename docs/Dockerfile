# Note: this Docker image is meant to be built using the root of the repository
# as context
# Note: the MetalK8s repository root is supposed to be mounted at
# `/usr/src/metalk8s` when running the container

FROM docker.io/alpine:3.8

WORKDIR /usr/src/metalk8s

RUN mkdir docs

RUN apk --no-cache add \
        enchant \
        git \
        make \
        py-twisted \
        py2-pip \
        && \
    pip install \
        tox \
        buildbot-worker==0.9.12

COPY tox.ini .
COPY docs/requirements.txt docs/

RUN tox --workdir /tmp/tox --notest -e docs

ENTRYPOINT ["tox", "--workdir", "/tmp/tox", "-e", "docs"]