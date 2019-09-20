FROM gcr.io/svctk-images/demo-go
RUN apk update && apk add git && apk add alpine-sdk && apk add ca-certificates && rm -rf /var/cache/apk/*
COPY go.* /modbuild/
WORKDIR /modbuild
ENV GOPROXY=https://proxy.golang.org
RUN go mod download
COPY *.go /modbuild/
RUN go build -o /app *.go

FROM alpine:3.9
CMD ["/app"]
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /app .
