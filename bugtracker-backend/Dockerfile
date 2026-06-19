FROM golang:1.21

WORKDIR /app

# install base tools (Debian-based image → NO apk)
RUN apt-get update && apt-get install -y \
    ca-certificates \
    git \
    wget \
 && rm -rf /var/lib/apt/lists/*

# copy go modules first (cache layer)
COPY go.mod go.sum ./
RUN go mod download

# copy source
COPY . .

# build
RUN go build -o main cmd/bugtracker/main.go

# runtime port
EXPOSE 8080

CMD ["./main"]
