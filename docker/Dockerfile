FROM fedora:41

LABEL maintainer="60469435+geugenm@users.noreply.github.com"
LABEL description="Minimal Fedora container for Ansible playbook execution"

RUN dnf -y update \
  && dnf -y install python3 python3-pip openssh-clients sshpass \
  sudo which tar unzip git \
  && python3 -m pip install --no-cache-dir ansible \
  && dnf clean all \
  && rm -rf /var/cache/dnf

# Create non-root user for better security
RUN useradd -m ansible \
  && echo "ansible ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/ansible

WORKDIR /ansible

COPY . /ansible/

RUN chown -R ansible:ansible /ansible

USER ansible

# Set Python to not write bytecode files to reduce disk usage
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV ANSIBLE_HOST_KEY_CHECKING=false

CMD ["bash"]
