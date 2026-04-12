FROM rust:1.80-slim-bookworm AS builder

# Install the latest tokei
RUN cargo install tokei

FROM debian:bookworm-slim

WORKDIR /workspace

COPY --from=builder /usr/local/cargo/bin/tokei /usr/local/bin/tokei

ENTRYPOINT ["tokei"]
