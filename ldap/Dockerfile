FROM debian:stable
LABEL maintainer=mlechner@bfs.de

RUN apt-get -y update
RUN apt-get -y install debconf-utils
RUN echo "slapd slapd/password1 password secret" | debconf-set-selections && \
    echo "slapd slapd/password2 password secret" | debconf-set-selections && \
    echo "slapd slapd/domain string gitlab.example.test" | debconf-set-selections && \
    echo "slapd slapd/root_dn string cn=admin,dc=gitlab,dc=example,dc=test" | debconf-set-selections && \
    apt-get -y install slapd
RUN apt-get -y clean

ENV BASE_DIR=/usr/local/gitlab_ldap

ADD . ${BASE_DIR}

RUN slapadd -l ${BASE_DIR}/users.ldif

CMD ["/usr/sbin/slapd", "-d", "0"]
