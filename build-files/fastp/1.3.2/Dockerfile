FROM ubuntu:noble AS app

RUN groupadd -r staphb && useradd -r -g staphb staphb

ARG FASTP_VER="1.3.2"

LABEL \
      # The date this image was last updated (Manually update this!)
      org.opencontainers.image.created="2026-04-08" \
      # The exact base image used for the 'app' stage (Must match the FROM instruction above)
      org.opencontainers.image.base.name="ubuntu:noble" \
      # The name of the software (e.g., "BWA" or "Samtools")
      org.opencontainers.image.title="fastp" \
      # The version of the software itself
      org.opencontainers.image.version="${FASTP_VER}" \
      # The version of THIS Dockerfile (increment if you change the build logic)
      org.opencontainers.image.revision="1" \
      # A human-readable description of the tool
      org.opencontainers.image.description="An ultra-fast all-in-one FASTQ preprocessor" \
      # The project homepage or GitHub repository
      org.opencontainers.image.url="https://github.com/StaPH-B/docker-builds" \
      # Where users can find instructions or manuals for the software
      org.opencontainers.image.documentation="https://github.com/OpenGene/fastp" \
      # Link to the source code used to build the image (which is often a GitHub url)
      org.opencontainers.image.source="https://github.com/OpenGene/fastp" \
      # The software license (e.g., MIT, GPL-3.0, Apache-2.0) for the software
      org.opencontainers.image.licenses="MIT" \
      # The person/group maintaining this Dockerfile
      org.opencontainers.image.authors="Kutluhan Incekara <kutluhan.incekara@ct.gov>, Raheel Ahmed <raheelsyedahmed@gmail.com>"

RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    ca-certificates \
    jq \
    python3 \
    python-is-python3 \
    procps && \
    apt-get autoclean && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/bin

RUN wget http://opengene.org/fastp/fastp.${FASTP_VER} && \
    mv fastp.${FASTP_VER} fastp && \
    chmod a+x ./fastp

RUN wget https://raw.githubusercontent.com/OpenGene/fastp/v${FASTP_VER}/parallel.py \
    -O /usr/local/bin/parallel.py && \
    chmod +x /usr/local/bin/parallel.py

ENV LC_ALL=C

WORKDIR /data

USER staphb

CMD [ "fastp", "--help" ]

FROM app AS test

WORKDIR /test


RUN fastp --help && \
    fastp --version

RUN jq --help && \
    jq --version

RUN parallel.py -h

# downloading sars-cov-2 fastq test files
RUN wget \
    https://raw.githubusercontent.com/StaPH-B/docker-builds/master/tests/SARS-CoV-2/SRR13957123_1.fastq.gz \
    https://raw.githubusercontent.com/StaPH-B/docker-builds/master/tests/SARS-CoV-2/SRR13957123_2.fastq.gz

# running fastp on the files
RUN fastp \
    -i SRR13957123_1.fastq.gz \
    -I SRR13957123_2.fastq.gz \
    -o SRR13957123_PE1.fastq.gz \
    -O SRR13957123_PE2.fastq.gz \
    -h SRR13957123_fastp.html \
    -j SRR13957123_fastp.json
