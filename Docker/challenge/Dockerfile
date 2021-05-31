FROM golang:latest AS builder

ENV GO111MODULE=on \
    CGO_ENABLED=1

WORKDIR /build

COPY . .

RUN go build ./hello.go

WORKDIR /dist
RUN cp /build/hello ./hello


FROM scratch
COPY --chown=0:0 --from=builder /dist /

ENTRYPOINT ["./hello"]
