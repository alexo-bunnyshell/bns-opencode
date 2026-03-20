FROM golang:1.24-bookworm AS builder

RUN go install github.com/opencode-ai/opencode@latest

FROM debian:bookworm-slim AS dev

RUN apt-get update && apt-get install -y --no-install-recommends \
    git curl bash ca-certificates wget \
    && wget -qO /usr/local/bin/ttyd https://github.com/tsl0922/ttyd/releases/download/1.7.7/ttyd.x86_64 \
    && chmod +x /usr/local/bin/ttyd \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /go/bin/opencode /usr/local/bin/opencode

WORKDIR /workspace

EXPOSE 7681

CMD ["sh", "-c", "ttyd -W -c ${TTYD_USER}:${TTYD_PASS} bash"]
