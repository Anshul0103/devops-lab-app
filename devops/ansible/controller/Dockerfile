FROM almalinux:9

RUN dnf install -y epel-release \
    && dnf install -y \
       ansible-core \
       openssh-clients \
       python3 \
    && dnf clean all

WORKDIR /ansible

CMD ["sleep", "infinity"]

