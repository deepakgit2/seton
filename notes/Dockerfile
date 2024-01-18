# @author: Deepak Singh

# Base Image
FROM ubuntu:20.04

# Env Vars
ENV TZ=Asia/Kolkata \
    DISPLAY=:99

# Install Packages
RUN apt update && DEBIAN_FRONTEND=noninteractive apt install -y tzdata git-all
# RUN apt update && \
    # Install tzdata for timezone (required for setting IST time)
    # DEBIAN_FRONTEND=noninteractive apt install -y tzdata git-all
    # Install Git 
    # DEBIAN_FRONTEND=noninteractive apt install -y git
    # Install Usefull Packages
    
RUN apt install -y nano zip wget curl net-tools iputils-ping && \
    # Git Configs
    git config --global user.email "singh.deepak3096@gmail.com" && \
    git config --global user.name "Deepak Singh" && \
    git config --global credential.helper 'cache --timeout=604800' && \
    # Install miniconda
    mkdir -p ~/miniconda3 && \
    wget https://repo.anaconda.com/miniconda/Miniconda3-py310_23.11.0-2-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh && \
    bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3 && \
    rm -rf ~/miniconda3/miniconda.sh && \
    ~/miniconda3/bin/conda init bash && \
    ~/miniconda3/bin/pip install pandas scikit-learn matplotlib


# RUN apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev libsqlite3-dev wget libbz2-dev
# RUN mkdir temp &&
#     cd temp &&
#     wget https://www.python.org/ftp/python/3.9.13/Python-3.9.13.tgz &&
#     tar -xf Python-3.9.13.tgz &&
#     cd Python-3.9.13 &&
#     ./configure --enable-optimizations &&
#     make -j $(nproc) &&
#     make altinstall &&
#     cd ../.. &&
#     rm -rf temp
# Install Python
    # apt install -y python3 python3-pip python-is-python3 && \