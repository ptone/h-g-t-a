FROM gcr.io/svctk-images/demo-go as builder
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
