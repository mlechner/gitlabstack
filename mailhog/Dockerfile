FROM golang:latest

LABEL maintainer=mlechner@bfs.de

RUN go install github.com/mailhog/MailHog@v1.0.1

CMD /go/bin/MailHog
