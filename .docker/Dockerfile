FROM golang:1.23-bookworm AS builder

RUN go install github.com/opencode-ai/opencode@latest

FROM debian:bookworm-slim AS dev

RUN apt-get update && apt-get install -y --no-install-recommends \
    git curl bash ttyd ca-certificates \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /go/bin/opencode /usr/local/bin/opencode

WORKDIR /workspace

EXPOSE 7681

CMD ["ttyd", "-W", "bash"]
