FROM jupyter/base-notebook:latest
ARG username="myuser"
ARG userid="1001"
ARG password="myuser123$%"
ENV NB_USER=$username \
    NB_UID=$userid \
    PASSWORD=$password \
    HOME=/home/$username
USER root
RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER && \
    usermod -aG sudo $NB_USER && \
    adduser $NB_USER sudo && \
    chmod  0440  /etc/sudoers && \
    echo 'myuser ALL=(ALL) ALL' >> /etc/sudoers && \
    chmod g+w /usr/sbin/chpasswd && \
    chmod g+w /etc/passwd && \
    echo "$NB_USER:$PASSWORD" | /usr/sbin/chpasswd
    
## changed start.sh script to use myuser as user
ADD ./start.sh /usr/local/bin/start.sh
RUN  chmod +x /usr/local/bin/start.sh
RUN mkdir -p "$HOME/work" && \
    fix-permissions "$HOME/work"
WORKDIR $HOME/work
USER $NB_UID