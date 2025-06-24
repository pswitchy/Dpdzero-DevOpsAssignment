FROM golang:1.22-alpine AS builder

WORKDIR /app

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o /app/main .

FROM scratch

COPY --from=builder /app/main /app/main

EXPOSE 8001

CMD ["/app/main"]