FROM golang:1.23.5-alpine AS builder

WORKDIR /app

RUN apk add --no-cache git

COPY go.mod go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .

FROM alpine:3.18

WORKDIR /root/

COPY --from=builder /app/main .

COPY --from=builder /app/.env .

EXPOSE 8008

CMD ["./main"]