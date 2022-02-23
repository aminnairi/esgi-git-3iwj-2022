FROM debian:11.2

RUN   apt-get update && \
      apt-get install --yes git openssh-server && \
      git config --global init.defaultBranch development && \
      mkdir -p /run/sshd && \
      mkdir -p /root/repository.git && \
      sed -i "s/#PermitRootLogin.*/PermitRootLogin yes/g" /etc/ssh/sshd_config && \
      sed -i "s/#PubkeyAuthentication.*/PubkeyAuthentication no/" /etc/ssh/sshd_config && \
      sed -i "s/#PasswordAuthentication.*/PasswordAuthentication yes/" /etc/ssh/sshd_config && \
      echo "root:root" | chpasswd && \
      git -C /root/repository.git init --bare

ENTRYPOINT ["/usr/sbin/sshd"]
CMD ["-D"]
