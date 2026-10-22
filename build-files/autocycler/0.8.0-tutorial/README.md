# autocycler container

Main tool: [autocycler](https://github.com/rrwick/Autocycler/)
  
Code repository: https://github.com/rrwick/Autocycler/

<details>

<summary>Additional tools installed via micromamba:</summary>

```
   Name                       Version               Build                   Channel    
 ────────────────────────────────────────────────────────────────────────────────────────
   _openmp_mutex              4.5                   20_gnu                  conda-forge
   _python_abi3_support       1.0                   hd8ed1ab_3              conda-forge
   about-time                 4.2.1                 pyhd8ed1ab_1            conda-forge
   alive-progress             3.3.0                 pyhd8ed1ab_0            conda-forge
   alsa-lib                   1.2.16.1              h7cc23a3_1              conda-forge
   archspec                   0.2.6                 pyhd8ed1ab_0            conda-forge
   autocycler                 0.8.0                 h79ce301_0              bioconda   
   backports.zstd             1.8.0                 py312h3f22e6b_0         conda-forge
   binutils                   2.46.1                default_h4852527_103    conda-forge
   binutils_impl_linux-64     2.46.1                default_hfdba357_103    conda-forge
   biopython                  1.88                  py312h5cc1888_1         conda-forge
   blast                      2.17.0                hb02a186_1              bioconda   
   boost-cpp                  1.85.0                h3c6214e_4              conda-forge
   brotli-python              1.2.0                 py312he9c40d5_4         conda-forge
   bwa                        0.7.19                h577a1d6_1              bioconda   
   bzip2                      1.0.8                 hda65f42_10             conda-forge
   c-ares                     1.34.9                hebe6cf0_0              conda-forge
   ca-certificates            2026.10.19            hbd8a1cb_0              conda-forge
   cairo                      1.18.4                h3394656_0              conda-forge
   canu                       2.3                   h636b4d1_3              bioconda   
   capnproto                  1.3.0                 h791c776_1              conda-forge
   certifi                    2026.10.19            pyhd8ed1ab_0            conda-forge
   tzdata                     2026c                 h151e31d_0              conda-forge
   unicycler                  0.5.1                 py312hdcc493e_5         bioconda   
   urllib3                    2.8.0                 pyhd8ed1ab_0            conda-forge
   wget                       1.25.0                h653f8fd_1              conda-forge
   wheel                      0.48.0                pyhd8ed1ab_0            conda-forge
   wtdbg                      2.5                   h577a1d6_6              bioconda   
   xcb-util                   0.4.1                 h4f16b4b_2              conda-forge
   xcb-util-image             0.4.0                 hb711507_2              conda-forge
   xcb-util-keysyms           0.4.1                 hb711507_0              conda-forge
   xcb-util-renderutil        0.3.10                hb711507_0              conda-forge
   xcb-util-wm                0.4.2                 hb711507_0              conda-forge
   xkeyboard-config           2.48                  h280c20c_0              conda-forge
   xorg-libice                1.1.2                 h280c20c_0              conda-forge
   xorg-libsm                 1.2.6                 h0d788c3_1              conda-forge
   xorg-libx11                1.8.14                hb83e432_0              conda-forge
   xorg-libxau                1.0.12                h7cc23a3_2              conda-forge
   xorg-libxdamage            1.1.6                 hb9d3cd8_0              conda-forge
   xorg-libxdmcp              1.1.5                 h7cc23a3_2              conda-forge
   xorg-libxext               1.3.7                 h7cc23a3_1              conda-forge
   xorg-libxfixes             6.0.2                 h7cc23a3_1              conda-forge
   xorg-libxi                 1.8.4                 h7cc23a3_0              conda-forge
   xorg-libxrandr             1.5.5                 h7cc23a3_1              conda-forge
   xorg-libxrender            0.9.13                h7cc23a3_0              conda-forge
   xorg-libxshmfence          1.3.3                 hb9d3cd8_0              conda-forge
   xorg-libxt                 1.3.1                 h7cc23a3_1              conda-forge
   xorg-libxtst               1.2.6                 h7cc23a3_0              conda-forge
   xorg-libxxf86vm            1.1.7                 hb03c661_0              conda-forge
   xz                         5.8.3                 ha02ee65_1              conda-forge
   xz-gpl-tools               5.8.3                 ha02ee65_1              conda-forge
   xz-tools                   5.8.3                 hb03c661_1              conda-forge
   yaml                       0.2.5                 hebe6cf0_3              conda-forge
   zlib                       1.3.2                 h25fd6f3_3              conda-forge
   zstd                       1.5.7                 hb78ec9c_7              conda-forge
```

</details>

Basic information on how to use this tool:
- executable: autocycler
- help: --help
- version: --version
- description: |
> Autocycler is a tool for generating consensus long-read assemblies for bacterial genomes.

Additional information:

This image does not contain any of the assemblers listed in the wikis or tutorials. All helper scripts should be in path and are located at /usr/local/bin.
  
Full documentation: [https://github.com/rrwick/Autocycler/wiki](https://github.com/rrwick/Autocycler/wiki)

## Official Steps
* Step 1: [Autocycler subsample](https://github.com/rrwick/Autocycler/wiki/Autocycler-subsample)
  * "Creates multiple read subsets from a single long-read dataset, minimising overlap to ensure each subset is as independent as possible."
* Step 2: [Generating input assemblies](https://github.com/rrwick/Autocycler/wiki/Generating-input-assemblies)
  * "Each of the read subsets made by Autocycler subsample can now be assembled, producing multiple alternative assemblies of the same genome."
* Step 3: [Autocycler compress](https://github.com/rrwick/Autocycler/wiki/Autocycler-compress)
  * "The autocycler compress command uses your input assemblies to build a compacted De Bruijn graph (a.k.a. a unitig graph)."
* Step 4: [Autocycler cluster](https://github.com/rrwick/Autocycler/wiki/Autocycler-cluster)
  * "The autocycler cluster command groups input contigs into clusters. A cluster is a group of contigs which represent the same genomic sequence. It also decides which of these clusters should be included in the final assembly (QC-pass) and which should not (QC-fail)."
* Step 5: [Autocycler trim](https://github.com/rrwick/Autocycler/wiki/Autocycler-trim)
  * "Long-read contigs sometimes contain excess sequence which needs to be trimmed off." 
  * "This step is performed on a per-cluster basis. For each contig, Autocycler looks for two types of excess sequence: start-end circular overlap and hairpin overlap. Contigs are trimmed as necessary. After trimming, Autocycler discards any contigs with outlier lengths, so the remaining contigs in the cluster will all be in close agreement with each other."
* Step 6: [Autocycler resolve](https://github.com/rrwick/Autocycler/wiki/Autocycler-resolve) \
"Aims to resolve repeats and ambiguities in the cluster by following these steps:

  * Identifying anchors: unitigs which occur exactly once in each of the cluster's contigs.
  * Creating bridges: connections between anchors that follow the most supported path.
  * Applying bridges: first unique bridges (those with no conflicts) and then the most supported conflicting bridges.
  * Merging linear sequences into 'consentigs'."

* Step 7: [Autocycler combine ](https://github.com/rrwick/Autocycler/wiki/Autocycler-combine)
  * "This is the final step in an Autocycler assembly, where the resolved sequences for each cluster are combined into a single assembly."

## Quick Start step with helper script.

```bash
autocycler_full.sh reads.fastq.gz 16 4
```

## Fully automated assembly

```bash
reads=ont.fastq.gz  # your read set goes here
threads=16  # set as appropriate for your system (no more than 128)
genome_size=$(autocycler helper genome_size --reads "$reads" --threads "$threads")  # can set this manually if you know the value

# Step 1: subsample the long-read set into multiple files
autocycler subsample --reads "$reads" --out_dir subsampled_reads --genome_size "$genome_size"

# Step 2: assemble each subsampled file
mkdir assemblies
for assembler in canu flye metamdbg miniasm necat nextdenovo plassembler raven; do
    for i in 01 02 03 04; do
        autocycler helper "$assembler" --reads subsampled_reads/sample_"$i".fastq --out_prefix assemblies/"$assembler"_"$i" --threads "$threads" --genome_size "$genome_size"
    done
done

# Optional step: remove the subsampled reads to save space
rm subsampled_reads/*.fastq

# Step 3: compress the input assemblies into a unitig graph
autocycler compress -i assemblies -a autocycler_out

# Step 4: cluster the input contigs into putative genomic sequences
autocycler cluster -a autocycler_out

# Steps 5 and 6: trim and resolve each QC-pass cluster
for c in autocycler_out/clustering/qc_pass/cluster_*; do
    autocycler trim -c "$c"
    autocycler resolve -c "$c"
done

# Step 7: combine resolved clusters into a final assembly
autocycler combine -a autocycler_out -i autocycler_out/clustering/qc_pass/cluster_*/5_final.gfa
```

## Information about manually curating your own assembly

According to the author, Ryan Wick, certain steps in the aforementioned fully automated assembly can be [manually curated](https://github.com/rrwick/Autocycler/wiki/Manually-curated-assembly).

* After Steps 1 & 2, you can curate input assemblies.
  * See the [Generating input assemblies](https://github.com/rrwick/Autocycler/wiki/Generating-input-assemblies) page for more details.
  * See the [Influencing Autocycler via contig headers](https://github.com/rrwick/Autocycler/wiki/Influencing-Autocycler-via-contig-headers) page for more details.
* After Steps 3 & 4, you can curate your clusters.
  * See the [Autocyler cluster](https://github.com/rrwick/Autocycler/wiki/Autocycler-cluster) page for more details.
* After Steps 5 & 6, you can examine dot plots and the autocycler bridging.
  * See the [Autocycler dotplot](https://github.com/rrwick/Autocycler/wiki/Autocycler-dotplot) page for more information.
  * "In particular, it can be helpful to examine each cluster's 4_merged.gfa file to see if there is structural heterogeneity or conflicts between assemblies."
* A manual step of removing any extraneous sequences can be done after Step 7.
  * See [Bandage](https://github.com/rrwick/Bandage), a tool by Ryan Wick.
  * [Autocycler clean](https://github.com/rrwick/Autocycler/wiki/Autocycler-clean) can be used to "remove unwanted tigs to allow for a fully resolved assembly."
