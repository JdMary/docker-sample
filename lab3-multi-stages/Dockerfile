# Build stage
FROM golang:latest AS builder
WORKDIR /go-http-hello-world/

# Initialize a Go module (needed for Go 1.11 and above)
RUN go mod init go-http-hello-world

# Get the required dependency (golang.org/x/net/html)
RUN go mod tidy

# Download the Go source file
RUN curl -o hello_world.go https://raw.githubusercontent.com/eliesjebri/DevOps/refs/heads/master/hello_world.go

# Build the Go app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

# Final minimal image stage
FROM scratch
COPY --from=builder /go-http-hello-world/app .
CMD ["./app"]

