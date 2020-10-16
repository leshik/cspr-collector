FROM golang:1.15.3-alpine3.12 as builder
WORKDIR /go/src
COPY . .
ENV CGO_ENABLED=0
ENV GOOS=linux
RUN go build -a -installsuffix cgo -o cspr-collector cmd/cspr-collector/main.go

FROM alpine:3.12
RUN apk add --no-cache ca-certificates
WORKDIR /app/
COPY --from=builder /go/src/cspr-collector .
EXPOSE 80
ENTRYPOINT ["./cspr-collector"]
