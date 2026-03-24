# Build stage
FROM golang:1.23-alpine AS builder

WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o dashboard .

# Runtime stage
FROM alpine:3.21

RUN adduser -D -g '' appuser

WORKDIR /app

COPY --from=builder /app/dashboard .

USER appuser

EXPOSE 8081

CMD ["./dashboard"]
