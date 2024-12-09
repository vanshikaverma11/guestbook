# Stage 1: Build stage
FROM golang:1.18 AS builder

# Set the working directory
WORKDIR /app

# Copy the Go source code to the build container
COPY main.go .

# Initialize the Go module and tidy dependencies
RUN go mod init guestbook
RUN go mod tidy

# Compile the Go program
RUN go build -o main main.go

# Stage 2: Production stage
FROM ubuntu:18.04

# Copy the compiled binary from the builder stage to the production container
COPY --from=builder /app/main /app/guestbook

# Copy static files to the container
COPY public/index.html /app/public/index.html
COPY public/script.js /app/public/script.js
COPY public/style.css /app/public/style.css
COPY public/jquery.min.js /app/public/jquery.min.js

# Set the working directory for the production container
WORKDIR /app

# Expose the application port
EXPOSE 3000

# Define the command to run the application
CMD ["./guestbook"]
