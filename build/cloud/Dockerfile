FROM golang:1.19.12-alpine3.17 AS builder

ARG GO_LDFLAGS

COPY . /go/src/github.com/kubeedge/kubeedge

RUN CGO_ENABLED=0 GO111MODULE=off go build -v -o /usr/local/bin/cloudcore -ldflags "$GO_LDFLAGS -w -s" \
    github.com/kubeedge/kubeedge/cloud/cmd/cloudcore


FROM alpine:3.17

COPY --from=builder /usr/local/bin/cloudcore /usr/local/bin/cloudcore

RUN apk add --update-cache \
    iptables \
    && rm -rf /var/cache/apk/*

ENTRYPOINT ["cloudcore"]
