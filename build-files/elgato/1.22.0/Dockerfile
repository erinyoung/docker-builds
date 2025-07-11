FROM staphb/ispcr:33 AS ispcr

## App ##
FROM ubuntu:jammy AS app

ARG ELGATO_VER="1.22.0"

LABEL base.image="ubuntu:jammy"
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

# copy precompiled ispcr from staphb image    
COPY --from=ispcr /usr/local/bin/isPcr /usr/local/bin/isPcr

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
RUN wget -q -P /usr/local/bin/ https://ftp.ncbi.nlm.nih.gov/pub/datasets/command-line/v2/linux-amd64/datasets &&\
    chmod 755 /usr/local/bin/datasets &&\
    datasets download genome accession GCF_900119765.1 --include genome &&\
    unzip -j ncbi_dataset.zip ncbi_dataset/data/GCF_900119765.1/GCF_900119765.1_2532STDY5467631_genomic.fna -d .

# test el_gato
RUN el_gato.py --assembly GCF_900119765.1_2532STDY5467631_genomic.fna --out test/ &&\
    cat test/run.log

# test reporting
RUN elgato_report.py -i test/report.json -o test/report.pdf
