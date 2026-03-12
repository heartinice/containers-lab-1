# Stage 1: Build
FROM golang:1.21-alpine AS builder
# Установка зависимостей для сборки
RUN apk add --no-cache git
# Рабочая директория
WORKDIR /app
# Копирование файлов зависимостей
COPY go.mod go.sum ./
# Загрузка зависимостей
RUN go mod download
# Копирование исходного кода
COPY . .
# Сборка приложения
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o main .
# Stage 2: Final
FROM alpine:latest
# Установка CA сертификатов для HTTPS
RUN apk --no-cache add ca-certificates
# Рабочая директория
WORKDIR /root/
# Копирование собранного приложения из builder
COPY --from=builder /app/main .
# Копирование статических файлов
COPY --from=builder /app/static ./static
# Экспонирование порта
EXPOSE 8080
# Запуск приложения
CMD ["./main"]