# Docker inheritance

# this is a ubuntu image with R, Rstudio and bioC
FROM bioconductor/bioconductor_docker:3.23-r-4.6.1

# Update apt-get
RUN apt-get update \
	&& apt-get install -y nano git \
	## Install the python package magic wormhole to send files
	&& pip install magic-wormhole		\
	## Remove packages in '/var/cache/' and 'var/lib'
	## to remove side-effects of apt-get update
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*


# Install required CRAN packages
RUN R -e 'install.packages(c("kableExtra","beeswarm","gplots","eulerr","rmdformats","RhpcBLASctl","RColorBrewer"))'

# Install required Bioconductor package
RUN R -e 'BiocManager::install(c("getDEE2","DESeq2", "topconfects","fgsea","clusterProfiler","mitch","sva","limma","edgeR","GSVA","org.Hs.eg.db","GSEABase","GSVAdata","Biobase",""))'

# Clone the repository that contains the research code and execute it
RUN  git clone https://github.com/markziemann/pathway_confint.git

# Set the container working directory
ENV DIRPATH /pathway_confint
WORKDIR $DIRPATH

# change folder permissions so user can work freely
RUN chmod -R 777 /pathway_confint
