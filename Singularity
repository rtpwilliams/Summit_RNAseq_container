BootStrap: docker
From: ubuntu:16.04

%files
    environment.yml

%post

    # install some system deps
    apt-get -y update
    apt-get -y install locales curl bzip2 less unzip git wget vim ant default-jdk
    # this is a X11 dep 
    apt-get -y install libxext6
    # tools to open PDF and HTML files
    apt-get -y install firefox xpdf
    # some extra devel libs
    apt-get -y install zlib1g-dev libssl-dev libpng-dev uuid-dev
    # other
    locale-gen en_US.UTF-8
    apt-get clean

    # download and install miniconda3
    curl -sSL -O https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
    bash Miniconda3-latest-Linux-x86_64.sh -p /opt/conda -b
    rm -fr Miniconda3-latest-Linux-x86_64.sh
    export PATH=/opt/conda/bin:$PATH
    conda update -n base conda

    # download software through environment.yml and set as default environment
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc
    echo "source activate summit_rnaseq" > ~/.bashrc
    /opt/conda/bin/conda env create -f environment.yml

%environment
    export PATH=/opt/conda/envs/summit_rnaseq/bin:$PATH
    export LANG=en_US.UTF-8
    export LANGUAGE=en_US:en
    export LC_ALL=en_US.UTF-8
    export XDG_RUNTIME_DIR=""
    export PATH=/opt/conda/bin:$PATH

%runscript
    exec "$@"
