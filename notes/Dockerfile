# @author: Deepak Singh

# Base Image
FROM ubuntu:20.04

# Args Vars
ARG MINICONDA_LINK=https://repo.anaconda.com/miniconda/Miniconda3-py310_23.11.0-2-Linux-x86_64.sh

# Env Vars
ENV TZ=Asia/Kolkata \
    DISPLAY=:99

RUN apt-get update && \
    # Install Packages
    DEBIAN_FRONTEND=noninteractive apt-get install expect tzdata -y && \
    # Install Packages
    apt-get install nano zip wget curl net-tools iputils-ping -y && \
    # Git Install and Configs
    DEBIAN_FRONTEND=noninteractive apt-get install git-all -y && \
    echo "echo \$GIT_PASS" > ~/.git-askpass.sh && chmod +x ~/.git-askpass.sh && \
    echo "export GIT_ASKPASS=~/.git-askpass.sh" >> ~/.bashrc && \
    # Install Miniconda
    mkdir -p ~/miniconda3 && \
    wget ${MINICONDA_LINK} -O ~/miniconda3/miniconda.sh && \
    bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3 && \
    rm -rf ~/miniconda3/miniconda.sh && \
    ~/miniconda3/bin/conda init bash && \
    ~/miniconda3/bin/conda config --set auto_activate_base false
