FROM python:3.9.20-slim-bullseye

RUN apt update && apt install -y sudo wget &&\
    python -m pip install ansible

ADD --chown=root:root ./ansible/ /opt/ansible/

WORKDIR /opt/ansible
RUN ansible-galaxy install -r requirements.yml -p /opt/ansible/roles &&\
    ansible-playbook --connection=local --inventory 127.0.0.1, play_spark_standalone_install.yml

WORKDIR /opt/hadoop/bin
ENV PATH=$PATH:/opt/hadoop/bin
ENV HADOOP_CONF_DIR=/opt/hadoop/etc/hadoop
