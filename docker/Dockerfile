FROM continuumio/miniconda3:4.10.3

ENV SAMTOOLS_VERSION 1.9
ENV BSALIGN_VERSION 1.2.1
ENV MINIMAP2_VERSION 2.24
ENV PYSAM_VERSION 0.17.0


RUN conda update conda

ADD . /app


# dependency install
RUN apt-get -y update && apt install -y build-essential bzip2 gcc g++ make zlib1g-dev wget libncurses5-dev liblzma-dev libbz2-dev


# pysam install
RUN pip install pysam==${PYSAM_VERSION}
ENV PATH="${PATH}:/opt/conda/envs/pysam/bin"


# minimap2 install
RUN conda install -c conda-forge -c bioconda -c defaults minimap2==${MINIMAP2_VERSION}


# samtools install  
RUN cd /opt/ \
	&& wget https://github.com/samtools/samtools/releases/download/${SAMTOOLS_VERSION}/samtools-${SAMTOOLS_VERSION}.tar.bz2 \
	&& tar -xjf samtools-${SAMTOOLS_VERSION}.tar.bz2 \
	&& rm -rf samtools-${SAMTOOLS_VERSION}.tar.bz2  \
	&& cd samtools-${SAMTOOLS_VERSION}/ \
	&& make && make install


# bsalign install
RUN cd /opt/ \
        && wget https://github.com/ruanjue/bsalign/archive/refs/tags/v${BSALIGN_VERSION}.tar.gz \
        && tar -xvf v${BSALIGN_VERSION}.tar.gz \
        && rm -rf v${BSALIGN_VERSION}.tar.gz  \
        && cd bsalign-${BSALIGN_VERSION}/ \
        && make

ENV PATH="${PATH}:/opt/bsalign-${BSALIGN_VERSION}/"


# fusion seeker install
RUN cd /opt/ \
        && git clone https://github.com/Maggi-Chen/FusionSeeker.git

ENV PATH="${PATH}:/opt/FusionSeeker/"
