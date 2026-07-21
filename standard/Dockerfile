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

RUN pip install --force-reinstall --no-cache-dir -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple/ "jupyterlab-v4-codio-ext==0.1.21"
RUN pip install --force-reinstall --no-cache-dir -i https://test.pypi.org/simple/ --extra-index-url https://pypi.org/simple/ "jupyter-collaboration-codio==4.1.4rc0"

# Expose Jupyter port
EXPOSE 8888
