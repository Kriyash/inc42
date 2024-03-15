# Use the official golang image
FROM golang:alpine AS build

# Set the current working directory inside the container
WORKDIR /app

# Copy the source code into the container
COPY . .

# Build the Go app
RUN go build -o hello .

# Use a minimal alpine image
FROM alpine:latest

# Copy the pre-built binary from the previous stage
COPY --from=build /app/hello .

# Expose port 9090
EXPOSE 9090

# Command to run the executable
CMD ["./hello-world.exe"]