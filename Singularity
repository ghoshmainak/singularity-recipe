Bootstrap: docker
From: ubuntu:18.04
 
%post
 
apt-get -y update
apt-get -y install net-tools
apt-get -y install curl wget
 
# Install conda and check the md5 sum provided on the download site
export CONDA_DIR=/opt/conda
export PATH=$CONDA_DIR/bin:$PATH
export MINICONDA_VERSION=4.9.2
export PYTHON_VER=py37
 
cd /tmp && \
wget --quiet https://repo.continuum.io/miniconda/Miniconda3-${PYTHON_VER}_${MINICONDA_VERSION}-Linux-x86_64.sh
echo "3143b1116f2d466d9325c206b7de88f7 *Miniconda3-${PYTHON_VER}_${MINICONDA_VERSION}-Linux-x86_64.sh" | md5sum -c -
/bin/bash Miniconda3-${PYTHON_VER}_${MINICONDA_VERSION}-Linux-x86_64.sh -f -b -p $CONDA_DIR
rm Miniconda3-${PYTHON_VER}_${MINICONDA_VERSION}-Linux-x86_64.sh
$CONDA_DIR/bin/conda config --system --prepend channels conda-forge
$CONDA_DIR/bin/conda config --system --set auto_update_conda false
$CONDA_DIR/bin/conda config --system --set show_channel_urls true
$CONDA_DIR/bin/conda install --quiet --yes conda="${MINICONDA_VERSION%.*}.*"
conda update --all --quiet --yes
conda clean -tipsy
 
conda install --quiet --yes \
    'notebook=6.0.3' \
    'numpy' \
    'pandas'


%environment
 
XDG_RUNTIME_DIR=""
PATH=/opt/conda/bin:${PATH}
