Bootstrap: docker
From: bioconductor/release_core2

%apprun R
exec R --vanilla "$@"

%apprun Rscript
exec Rscript --vanilla "$@"

%runscript
exec R --vanilla "$@"

%post
apt-get update

# Basic dependencies for Seurat and most R packages
apt-get install -y apt-transport-https apt-utils software-properties-common
apt-get install -y curl wget nano libboost-all-dev libudunits2-dev gawk
apt-get install -y libblas3 libblas-dev liblapack-dev liblapack3 curl
apt-get install -y gcc fort77 aptitude
apt-get install -y g++
apt-get install -y xorg-dev
apt-get install -y libreadline-dev
apt-get install -y gfortran
gfortran --version
apt-get install -y libssl-dev libxml2-dev libpcre3-dev liblzma-dev libbz2-dev libcurl4-openssl-dev 
apt-get install -y libhdf5-dev hdf5-helpers libmariadb-client-lgpl-dev python3-pip python-pip  python-virtualenv

# Dependencies for rgl package
apt-get install -y xorg libglu1-mesa-dev libx11-dev libfreetype6-dev

# Dependencies for umap, monocle, phate (included into Seurat) and Magic.
pip install umap-learn 
pip install louvain
pip3 install umap-learn 
pip3 install louvain
pip3 install GPy

# installing packages from cran
R --slave -e 'install.packages("devtools",repos="https://cran.rstudio.com/")'
R --slave -e 'install.packages("dplyr",repos="https://cran.rstudio.com/")'
R --slave -e 'install.packages("Seurat",repos="https://cran.rstudio.com/")'

# Some monocle3 dependencies
R --slave -e 'install.packages("BiocManager");BiocManager::install();BiocManager::install(c("BiocGenerics", "DelayedArray", "DelayedMatrixStats","limma", "S4Vectors", "SingleCellExperiment","SummarizedExperiment"));devtools::install_github('cole-trapnell-lab/monocle3')'