FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive

### Basics ###

# Install basic dependencies
RUN apt-get update
RUN apt-get install -y wget curl apt-utils

# Install build tools
RUN apt-get install -y build-essential rustc cmake ninja-build pkg-config
RUN apt-get install -y gcc g++
RUN apt-get install -y libunwind-dev
RUN apt-get install -y python3 python3-pip python3-venv
RUN apt-get install -y nodejs npm

# Install git
RUN apt-get install -y git git-lfs
RUN git lfs install

### Profiling Tools ###
RUN python3 -m pip install py-spy --break-system-packages

### Development Tools ###

# Miniforge
RUN wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-aarch64.sh -O /tmp/miniforge.sh
RUN chmod +x /tmp/miniforge.sh
RUN bash /tmp/miniforge.sh -b -p /opt/conda
RUN rm /tmp/miniforge.sh

# Set Conda environment variables: Available but not activated
ENV PATH="/opt/conda/bin:$PATH"
RUN conda init && conda config --set auto_activate_base false

### Drivers (Partition-specific) ###

# Add Coral TPU repository
RUN echo "deb https://packages.cloud.google.com/apt coral-edgetpu-stable main" | tee /etc/apt/sources.list.d/coral-edgetpu.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update
RUN apt-get install -y libedgetpu1-std
