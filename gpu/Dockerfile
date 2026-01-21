FROM quay.io/jupyter/base-notebook:latest

USER root

# Install system dependencies
RUN apt-get update && apt-get install -y \
  git \
  wget \
  build-essential \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

USER ${NB_UID}

# Install PyTorch with CUDA 12.1 support
# RUN pip install --no-cache-dir \
#   torch torchvision --index-url https://download.pytorch.org/whl/cu121

# Copy requirements and install Python packages
COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# Expose Jupyter port
EXPOSE 8888
