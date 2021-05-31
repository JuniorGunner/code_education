FROM golang:latest AS builder

# TODO: essential components from golang image
ENV GO111MODULE=on \
    CGO_ENABLED=1

# COPY go.mod .
# COPY go.sum .
# RUN go mod download
RUN go mod init codeeducation.com/hello
RUN unset GOPATH
# RUN go mod vendor
RUN go build hello.go

COPY . .

# RUN go build ./hello.go

FROM scratch
COPY --chown=0:0 --from=builder . .

ENTRYPOINT ["./hello.go"]
# CMD go run hello.g
