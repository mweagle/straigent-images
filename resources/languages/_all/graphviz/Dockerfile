FROM debian:bookworm-slim

WORKDIR /workspace

RUN apt-get update \
    && apt-get install -y --no-install-recommends graphviz \
    && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["dot"]
