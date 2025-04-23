# Use an official Golang image as a parent image
FROM golang:1.18.2

# Set the working directory inside the container
WORKDIR /go/src/app

# Copy the local package files to the container's workspace
COPY . .

# Build the Go app
RUN export GO111MODULE=on
RUN go mod init github.com/bortizf/microservice-app-example/tree/master/auth-api
RUN go mod tidy
RUN go build -o main .

# Expose port 8083 to the outside world
EXPOSE 8000

# Command to run the application
CMD ["./main"]