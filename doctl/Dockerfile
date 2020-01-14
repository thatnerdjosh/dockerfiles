FROM digitalocean/doctl as builder
RUN adduser -D doctl 

FROM scratch
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
COPY --from=builder /app/doctl /doctl
COPY --from=builder /etc/passwd /etc/passwd
USER doctl
ENTRYPOINT ["/doctl"]
