# f5-ansible:dev - Dockerfile
# https://github.com/ArtiomL/f5-ansible
# Artiom Lichtenstein
# v1.0.2, 02/02/2018

FROM alpine

LABEL maintainer="Artiom Lichtenstein" version="1.0.2"

# Core dependencies
RUN apk add --update --no-cache gcc git libc-dev libffi libffi-dev make openssl openssl-dev py-pip python2-dev && \
	pip install bigsuds f5-sdk netaddr deepdiff && \
	pip install git+https://github.com/ansible/ansible.git && \
	apk del gcc git libc-dev libffi libffi-dev make openssl-dev python2-dev && \
	rm -rf /var/cache/apk/*

# Ansible
COPY / /opt/ansible/
RUN echo "deprecation_warnings = False" >> /opt/ansible/ansible.cfg
WORKDIR /opt/ansible/

# System account
RUN adduser -u 1001 -D user
RUN chown -RL user: /opt/ansible/

# UID to use when running the image and for CMD
USER 1001

# Run
CMD ["/bin/sh"]
