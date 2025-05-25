# Этап сборки
FROM golang:1.24-alpine AS builder

# Создаём рабочую директорию внутри контейнера
WORKDIR /app

# Копируем go.mod и go.sum и скачиваем зависимости
COPY go.mod go.sum ./
RUN go mod download

# Копируем весь код приложения в контейнер
COPY . .

# Собираем бинарник приложения (main.go в cmd/feed-service)
RUN go build -o feed-service .

# --- Второй этап: минимальный runtime образ ---
FROM alpine:latest

# Копируем бинарник из предыдущего шага
COPY --from=builder /app/feed-service /feed-service

# Открываем порт, на котором приложение будет слушать (например, 8080)
EXPOSE 8080

# Запускаем приложение
CMD ["/feed-service"]
