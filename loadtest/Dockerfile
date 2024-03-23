FROM rust:latest@sha256:00e330d2e2cdada2b75e9517c8359df208b3c880c5e34cb802c120083d50af35 AS builder

WORKDIR /app
COPY . .
RUN cargo install diesel_cli && cargo build --bin router --release

FROM rust:latest@sha256:00e330d2e2cdada2b75e9517c8359df208b3c880c5e34cb802c120083d50af35 AS runtime
WORKDIR /app
COPY --from=builder /app/migrations migrations
COPY --from=builder /app/target/release/router router
COPY --from=builder /usr/local/cargo/bin/diesel diesel
