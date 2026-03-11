FROM quay.io/jupyter/base-notebook:x86_64-python-3.13

USER root

# Install system dependencies
RUN apt-get update && apt-get install -y \
  git \
  wget \
  build-essential \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

USER ${NB_UID}

# Copy requirements and install Python packages
COPY --chown=${NB_UID}:${NB_GID} requirements.txt /tmp/
RUN pip install --no-cache-dir -r /tmp/requirements.txt

# Expose Jupyter port
EXPOSE 8888
