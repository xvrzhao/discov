FROM golang:alpine AS builder
RUN go env -w GO111MODULE=on GOPROXY=https://goproxy.io,direct
WORKDIR /app/src
COPY ./go.mod ./go.sum ./
RUN go mod download
COPY ./ ./
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /app/bin/app ./examples/k8s/client

FROM alpine
COPY --from=builder /app/bin/app /
ENTRYPOINT ["/app"]