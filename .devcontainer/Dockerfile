FROM mcr.microsoft.com/devcontainers/anaconda:0-3

# NOT SURE IF NECESSARY
# Copy environment.yml (if found) to a temp location so we update the environment.
COPY environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/

# Update the Anaconda environment
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then \
        umask 0002 && /opt/conda/bin/conda env update -n base -f /tmp/conda-tmp/environment.yml; \
    fi \
    && rm -rf /tmp/conda-tmp

# Install additional OS packages if needed
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

#Install additional packages
RUN conda install -y pandas numpy matplotlib seaborn jupyter ipykernel

# Activate the base environment
SHELL ["/bin/bash", "-c", "source activate base"]

# Copy your Jupyter Notebook file to a desired location inside the container
COPY analysis.ipynb /root/

# Set the working directory
WORKDIR /root/

# Set the default command to launch the Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
