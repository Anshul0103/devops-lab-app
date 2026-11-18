FROM almalinux:9

RUN dnf install -y \
    openssh-server \
    python3 \
    sudo \
    && dnf clean all

RUN useradd -m -s /bin/bash ansible \
    && echo "ansible ALL=(ALL) NOPASSWD: ALL " \
       > /etc/sudoers.d/ansible \
    && chmod 440 /etc/sudoers.d/ansible

RUN mkdir -p /home/ansible/.ssh

COPY ssh/authorized_keys /tmp/authorized_keys

RUN install -o ansible -g ansible -m 600 \
    /tmp/authorized_keys \
    /home/ansible/.ssh/authorized_keys \
    && chown ansible:ansible /home/ansible/.ssh \
    && chmod 700 /home/ansible/.ssh

RUN echo "PermitRootLogin no" > /etc/ssh/sshd_config.d/00-lab.conf \
    && echo "PasswordAuthentication no" >> /etc/ssh/sshd_config.d/00-lab.conf \
    && echo "PubkeyAuthentication yes" >> /etc/ssh/sshd_config.d/00-lab.conf \
    && echo "AllowUsers ansible" >> /etc/ssh/sshd_config.d/00-lab.conf \
#    && ssh-keygen -A \
    && mkdir -p /run/sshd

EXPOSE 22

#CMD ["/usr/sbin/sshd", "-D", "-e"]
CMD ["/bin/bash", "-lc", "ssh-keygen -A && exec /usr/sbin/sshd -D -e"]
