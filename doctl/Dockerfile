FROM digitalocean/doctl as builder
RUN adduser -D doctl 

FROM scratch
COPY --from=builder /app/doctl /doctl
COPY --from=builder /etc/passwd /etc/passwd
ENTRYPOINT ["/doctl"]
