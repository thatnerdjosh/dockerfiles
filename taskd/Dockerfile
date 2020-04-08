FROM alpine:3.8 as builder
RUN adduser -D taskd
RUN set -x                && \ 
    apk --update upgrade  && \
    apk add taskd         && \
    chown taskd:taskd /usr/bin/task*
RUN ldd /usr/bin/taskd | tr -s '[:blank:]' '\n' | grep '^/' | \
    xargs -I % sh -c 'mkdir -p $(dirname deps%); cp % deps%;'

FROM scratch
COPY --from=builder /deps /
COPY --from=builder /usr/bin/taskd /usr/bin/taskd
COPY --from=builder /etc/passwd /etc/passwd
USER taskd
ENTRYPOINT ["/usr/bin/taskd"]
