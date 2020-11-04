FROM nvcr.io/nvidia/tensorflow:20.09-tf1-py3

WORKDIR /home

# dfl requirements
RUN git clone https://github.com/nagadit/DeepFaceLab_Linux.git /home
RUN git clone https://github.com/iperov/DeepFaceLab.git /home/deepfacelab
RUN pip install opencv-python ffmpeg-python scikit-image scipy colorama labelme pyqt5
RUN apt-get -y install ffmpeg

RUN set '2d' /home/scripts/env.sh
RUN sed -i '/export DFL_WORKSPACE=/c\export DFL_WORKSPACE="/home/workspace"' /home/scripts/env.sh
RUN sed -i '/export DFL_SRC=/c\export DFL_SRC="/home/deepfacelab"' /home/scripts/env.sh
RUN sed -i '/export DFL_ROOT=/c\export DFL_ROOT="home/deepfacelab"' /home/scripts/env.sh

RUN sed -i '/rm -r/c\rm -rf "$DFL_WORKSPACE/*"' /home/scripts/1_clear_workspace.sh

# enable ssh
RUN apt-get -y update
RUN apt-get -y install openssh-server

# allow root login, you will need change root password by passwd root
RUN echo "PermitRootLogin yes" >> /etc/ssh/sshd_config
RUN echo "ForwardX11 yes" >> /etc/ssh/sshd_config
RUN echo "ForwardX11Trusted yes" >> /etc/ssh/sshd_config

EXPOSE 22
EXPOSE 6000 # for x11 forwarding
VOLUME /home/workspace

ENTRYPOINT service ssh start && /bin/bash

# you will need change root password by following command
# docker ps
# docker exec -it [containerid] /bin/bash
# passwd root
~                         
