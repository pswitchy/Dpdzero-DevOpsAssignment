FROM golang:1.22-alpine AS builder

WORKDIR /app

COPY . .

RUN go mod init service1 && \
    CGO_ENABLED=0 GOOS=linux go build -o main .

FROM alpine:latest

RUN apk --no-cache add ca-certificates wget

WORKDIR /root/

COPY --from=builder /app/main .

EXPOSE 8001

CMD ["./main"]