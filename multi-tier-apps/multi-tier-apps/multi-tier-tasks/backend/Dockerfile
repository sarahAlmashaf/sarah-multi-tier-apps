FROM golang:1.22-alpine as builder

WORKDIR /app

COPY . .

COPY ca-certs/*.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

RUN go build -o main .


# minimal scratch base image, Contains only the compiled binary and no additional packages or libraries.
FROM scratch

COPY --from=builder /app/main /app/main

USER 1000:1000

EXPOSE 8080


CMD ["/app/main"]


