FROM golang:1.24-bookworm AS build

ARG CUE_VERSION=v0.14.2

WORKDIR /src

RUN GOBIN=/out go install cuelang.org/go/cmd/cue@${CUE_VERSION}

FROM debian:bookworm-slim

WORKDIR /workspace

COPY --from=build /out/cue /usr/local/bin/cue

ENTRYPOINT ["cue"]
