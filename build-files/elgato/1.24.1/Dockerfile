ARG ELGATO_VER="1.24.1"
ARG ISPCR_VER="33"

FROM ubuntu:noble as builder

ARG ISPCR_VER
ARG MACHTYPE="x86_64-pc-linux-gnu"

RUN apt-get update && apt-get install -y \
    build-essential \
    wget \
    unzip

RUN wget https://hgwdev.gi.ucsc.edu/~kent/src/isPcr${ISPCR_VER}.zip &&\
    unzip isPcr${ISPCR_VER}.zip &&\
    cd isPcrSrc &&\
    sed -i 's/-Werror//g' inc/common.mk &&\
    mkdir -p bin/$MACHTYPE &&\
    mkdir -p lib/$MACHTYPE &&\
    make HOME=$PWD MACHTYPE=${MACHTYPE} C_INCLUDE_PATH=/usr/include LIBRARY_PATH=/usr/lib CFLAGS="-fcommon" &&\
    mv bin/$MACHTYPE/* /usr/local/bin/

FROM ubuntu:noble AS app

ARG ELGATO_VER

LABEL base.image="ubuntu:noble"
LABEL dockerfile.version="1"
LABEL software="el_gato"
LABEL software.version="${ELGATO_VER}"
LABEL description="Epidemiology of Legionella : Genome-bAsed Typing"
LABEL website="https://github.com/CDCgov/el_gato"
LABEL license="https://github.com/CDCgov/el_gato/blob/main/LICENSE"
LABEL maintainer="Kutluhan Incekara"
LABEL maintainer.email="kutluhan.incekara@ct.gov"

# dependencies
RUN apt-get update && apt-get install --no-install-recommends -y \
    wget \
    python3-pip \
    minimap2 \
    samtools \
    ncbi-blast+ && \
    apt-get autoclean && rm -rf /var/lib/apt/lists/*

# copy precompiled ispcr from builder stage    
COPY --from=builder /usr/local/bin/* /usr/local/bin/

# install el_gato
RUN wget --no-check-certificate https://github.com/CDCgov/el_gato/archive/refs/tags/${ELGATO_VER}.tar.gz &&\
    tar -xvf ${ELGATO_VER}.tar.gz && rm ${ELGATO_VER}.tar.gz &&\
    cd el_gato-${ELGATO_VER} &&\
    python3 -m pip install . --no-cache-dir &&\
    mv ./el_gato/db/ /usr/local/bin/db/

# install fpd2 for pdf reports    
RUN pip install --no-cache-dir fpdf2 packaging

ENV LC_ALL=C

CMD ["el_gato.py", "-h"]

WORKDIR /data

## Test ##
FROM app AS test

RUN apt-get update && apt-get install unzip 

# download Legionella pneumophila ST62 genome
RUN wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/900/119/765/GCF_900119765.1_2532STDY5467631/GCF_900119765.1_2532STDY5467631_genomic.fna.gz &&\
    gunzip GCF_900119765.1_2532STDY5467631_genomic.fna.gz

# test el_gato
RUN el_gato.py --assembly GCF_900119765.1_2532STDY5467631_genomic.fna --out test/ &&\
    cat test/run.log

# test reporting
RUN elgato_report.py -i test/report.json -o test/report.pdf
