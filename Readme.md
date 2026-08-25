<div align="center"><img alt="image" src="https://github.com/user-attachments/assets/729a8e17-94a4-492a-8d01-c902303c06a1" width=45%/></div>

---
## Introduction（CPhasing）
⭐️[CPhasing original github](https://github.com/wangyibin/CPhasing)   
One of the major problems with Hi-C scaffolding of polyploid genomes is a large proportion of ambiguous short-read mapping, leading to a high-level of switched or chimeric assemblies. Now, the long-read-based chromosome conformation capture technology, e.g., **Pore-C**, **HiFi-C**(**CiFi**), provides an effective way to overcome this problem. Here, we developed a new pipeline, namely `C-Phasing`, which is specifically tailored for polyploid phasing by leveraging the advantage of Pore-C or HiFi-C data. It also works on **Hi-C** or **Omni-C** data and **diploid** genome assembly.  
  
The advantages of `C-Phasing`:   
- High speed.   
- High anchor rate of genome. 
- High accuracy of polyploid phasing. 

![Summary_of_CPhasing](https://github.com/wangyibin/CPhasing/blob/main/pictures/Summary_of_CPhasing.png)

More details please check the documentation:  
[Documentation](https://wangyibin.github.io/CPhasing/) | [中文文档](https://wangyibin.github.io/CPhasing/zh)


# Introduction（CPhasing-mod）
`CPhasing-mod` is a modified version of `C-Phasing`, featuring the following enhancements:

1️⃣ Refactor the `nextflow + shell` pipeline to improve script readability and maintainability.

2️⃣ Support simultaneous Hi-C/Pore-C clustering analysis across multiple data types, including but not limited to:
`minibwa`, `bwa-mem2`, `_chromap`, `chromap`, `pairs.gz`, and `bam` formats. The pipeline should generate multiple outputs such as `.agp`, `.hic`, and `.assembly` files accordingly.

3️⃣ Enable cross-compatibility among multiple `.assembly` files — they can share the same `.hic` file, while different `.hic` files differ only in interaction signal intensity, not in the underlying assembly structure.

4️⃣ Support both `local` execution and `slurm` cluster deployment, ensuring seamless job scheduling and resource management across environments.

5️⃣ Provide enhanced resumption capabilities for convenient continuation of interrupted runs, minimizing redundant computation and facilitating incremental updates.

⭐️If you encounter any issues, feel free to ask in the issue section. Please also support the original authors. **If you use `CPhasing-mod`, kindly cite it:**   

- **C-Phasing**
    > Yibin Wang, Ping Zhao, Xiaofei Zeng, Jiaxin Yu, Aoqian Dong, Yi Liu, Mengwei Jiang, Fang Wang, Xiao Chen, Shengcheng Zhang, Shuai Chen, Yuqing Gong, Yixing Zhang, Ruicai Long, Maojun Wang, Haibao Tang and Xingtan Zhang. Enhanced Pore-C with C-Phasing Enables Chromosomal-Scale, Haplotype-Resolved Assembly of Ultra-Complex Genomes, 05 November 2025, PREPRINT (Version 1) available at Research Square [https://doi.org/10.21203/rs.3.rs-7343323/v1]

- And HapHiC:
    > Xiaofei Zeng, Zili Yi, Xingtan Zhang, Yuhui Du, Yu Li, Zhiqing Zhou, Sijie Chen, Huijie Zhao, Sai Yang, Yibin Wang, Guoan Chen. Chromosome-level scaffolding of haplotype-resolved assemblies using Hi-C data without reference genomes. Nature Plants, 10:1184-1200. doi: https://doi.org/10.1038/s41477-024-01755-3

- And ALLHiC
    > Xingtan Zhang, Shengcheng Zhang, Qian Zhao, Ray Ming, Haibao Tang. (2019) Assembly of allele-aware, chromosomal-scale autopolyploid genomes based on Hi-C data. Nature Plants, 5:833-845. doi: https://doi.org/10.1038/s41477-019-0487-8

---

# Other modified versions of the software
⭐️ For the modified version of annotation tool `EviAnn`, please visit: [EviAnn-mod](https://github.com/linyuiz/EviAnn-mod) (Not recommended for now, currently under upgrade)  

⭐️ For the modified version of TE transposon annotation tool `EDTA`, please visit: [EDTA-mod](https://github.com/linyuiz/EDTA-mod) (Beta version)  

⭐️ For the modified version of scaffolding tool `C-Phasing`, please visit: [CPhasing-mod](https://github.com/linyuiz/CPhasing-mod) (Beta version)   

---

# Installation
## Install with conda/mamba (Linux64) 
To install, first download the latest distribution tarball：[zgtools-CPhasing-mod_*.tar.gz](https://github.com/linyuiz/CPhasing-mod/releases/download/v0.1/zgtools-CPhasing-mod_v0.1.tar.gz) (not one of the Source code files!) from the github release page：https://github.com/linyuiz/CPhasing-mod/releases/. 

```shell
#1. CPhasing install
##mkdir -p ~/software && cd ~/software
mamba create -n cphasing && conda activate cphasing
wget -c https://github.com/wangyibin/CPhasing/releases/download/v0.3.2/CPhasing.v0.3.2.r312.linux-64.tar.gz
tar -zxvf CPhasing.v0.3.2.r312.linux-64.tar.gz && cd CPhasing_v0.3.2
sed -i '1d' environment.yml && mamba env update -f environment.yml
mamba install fastp networkx=3.4.2
#2. download 3D-DNA
##cd ~/software
wget -c https://github.com/aidenlab/3d-dna/archive/refs/tags/201008.tar.gz
tar -zxvf 3d-dna-201008.tar.gz 
#3. nextflow install
mamba create -n nextflow -c conda-forge -c bioconda nextflow==22.10.6
#4. zgtools CPhasing-mod install
tar -zxvf zgtools-CPhasing-mod_v0.1.tar.gz && cd zgtools-CPhasing-mod_v0.1 && chmod +x zg*
#5. add zgtools to your $PATH:
echo "export PATH=$PWD:\$PATH" >>~/.bashrc && source ~/.bashrc
zgtools CPhasing-mod
```
---

# Usage

You just need to soft link zgtools to your usual bin folder such as【~/bin】, or use an absolute path such as【/project/softawre/zgtools CPhasing-mod】.
```shell
Usage:

        zgtools CPhasing-mod Run_CPhasing.cfg

        Run_CPhasing.cfg   --Run Config

Example1:

        zgtools CPhasing-mod example_cfg

Example2:

        zgtools CPhasing-mod Run_CPhasing.cfg
       
Example3:

        zgtools CPhasing-mod help
```
⭐️Note that the total Threads are threads multiplied by Parallel Task Num, for example: 60 x 3 = 180 threads.    

---

# Example
1️⃣ First, run `zgtools CPhasing-mod example_cfg` to generate a sample configuration file, then modify the parameters below according to your needs:
```
##Info
☆data_work_mode=local                        #local or slurm
☆data_genome_fa=00.data/genome.fa            #genome file
data_fastp_run_mode=yes                       #whether fastp filter HiC data(yes|no)
data_3ddna_run_mode=yes                       #whether create .hic file(yes|no)
☆data_parallel_task_num=2                    #parallel task num
☆data_each_group_chr_num=27                  #each group chr number
☆data_total_group_number=1                   #total group number
##Fastp
fastp_threads=16                              #fastp threads
##C-Phasing
☆cphasing_hyperpartition_mode=haploid        #hyperpartition mode(haploid|phasing)
☆cphasing_hic_aligner=_chromap               #chromap|bwa-mem2|minibwa
☆cphasing_threads=30                         #number of threads
☆cphasing_restriction_enzyme=GATC            #REs: GATC|AAGCTT
☆cphasing_input_hic_R1=00.data/hic_R1.fq.gz  #Hi-C data read1(R1.fq.gz)
☆cphasing_input_hic_R2=00.data/hic_R2.fq.gz  #Hi-C data read2(R2.fq.gz)
cphasing_input_pairs=none                     #4DN pairs file(input.pairs.gz)
cphasing_input_bam=none                       #pre-align bam file(input.align.bam)
cphasing_input_porec=none                     #Pore-C/CiFi data(FASTX[.gz]|BAM)
cphasing_hic_mapper_k=17                      #mapper's kmer size(>8G, use 27)
cphasing_hic_mapper_w=7                       #mapper's window size>8G, use 14)
cphasing_hcr_mode=yes                         #retain high confident area(yes|no)
cphasing_hyperpartition_q1=0                  #first cluster min quality(0<=x<=60)
cphasing_hyperpartition_q2=1                  #second cluster min quality(0<=x<=60)
cphasing_scaffolding_method=precision         #scaf_method(cphasing|allhic|fast)
cphasing_plot_binsize=auto                    #bin size of the heatmap(100k|500k|1m)
cphasing_plot_colormap=whitered               #colormap(redp1_r_half|whitered)
cphasing_plot_balance=yes                     #balance the matrix(yes|no)
cphasing_plot_whitered=yes                    #--scale none -cmap whitered(yes|no)
cphasing_plot_no_lines=no                     #whether use --no-lines(yes|no)
cphasing_plot_add_hap_border=yes              #whether add hap border(yes|no)
cphasing_plot_avoid_overlap_yticks=yes        #whether avoid overlap y-ticks(yes|no)
cphasing_plot_fontsize=auto                   #heatmap figure font size(auto|5|10)
cphasing_plot_dpi=300                         #plot figure dpi(150|300)
cphasing_low_memory=yes                       #reduce memory hyperpartition(yes|no)
##3D-DNA
3ddna_mapq=1                                  #build map for a specific mapq(0|1)
3ddna_java_xms=50G                            #java initial heap size
3ddna_java_xmx=750G                           #java maximum heap size
3ddna_min_resolutions=5000                    #minimum resolutions(1000|5000|10000)
3ddna_clean_run_mode=no                       #clean up when done(yes|no)
##CondaEnv
cphasing_env_name=cphasing                    #C-Phasing env name
nextflow_env_name=nextflow                    #nextflow env name
conda_path=~/miniconda3                       #conda envs path
cphasing_path=~/software/CPhasing_v0.3.2      #C-Phasing software path
3ddna_path=~/software/3d-dna-201008           #3D-DNA software path
```
2️⃣ Then, run `zgtools CPhasing-mod example_cfg`. If want to stop the job, please press `Ctrl + C`, not​ `Ctrl + Z`.            

# Run log

This is the command【`zgtools CPhasing-mod Run_CPhasing.cfg`】runtime log:   
```
#######Data#######
##Info
☆data_work_mode=slurm                        #local or slurm
☆data_genome_fa=00.data/genome.fa            #genome file
data_fastp_run_mode=yes                       #whether fastp filter HiC data(yes|no)
data_3ddna_run_mode=yes                       #whether create .hic file(yes|no)
☆data_parallel_task_num=2                    #parallel task num
☆data_each_group_chr_num=27                  #each group chr number
☆data_total_group_number=1                   #total group number
##Fastp
fastp_threads=16                              #fastp threads
##C-Phasing
☆cphasing_hyperpartition_mode=haploid        #hyperpartition mode(haploid|phasing)
☆cphasing_hic_aligner=_chromap,minibwa,bwa-mem2  #chromap|bwa-mem2|minibwa
☆cphasing_threads=30                         #number of threads
☆cphasing_restriction_enzyme=GATC            #GATC|AAGCTT
☆cphasing_input_hic_R1=00.data/hic_R1.fq.gz  #Hi-C data read1
☆cphasing_input_hic_R2=00.data/hic_R2.fq.gz  #Hi-C data read2
cphasing_input_pairs=none                     #4DN pairs file
cphasing_input_bam=none                       #pre-align bam file
cphasing_input_porec=none                     #Pore-C/CiFi data(FASTX[.gz]|BAM)
cphasing_hic_mapper_k=17                      #mapper's kmer size(>8G, use 27)
cphasing_hic_mapper_w=7                       #mapper's window size>8G, use 14)
cphasing_hcr_mode=yes                         #retain high confident area(yes|no)
cphasing_hyperpartition_q1=0                  #first cluster min quality(0<=x<=60)
cphasing_hyperpartition_q2=1                  #second cluster min quality(0<=x<=60)
cphasing_scaffolding_method=precision         #cphasing|allhic|fast
cphasing_plot_binsize=auto                    #bin size of the heatmap(100k|500k|1m)
cphasing_plot_colormap=whitered               #redp1_r_half|whitered
cphasing_plot_balance=yes                     #balance the matrix(yes|no)
cphasing_plot_whitered=yes                    #--scale none -cmap whitered(yes|no)
cphasing_plot_no_lines=no                     #whether use --no-lines(yes|no)
cphasing_plot_add_hap_border=yes              #whether add hap border(yes|no)
cphasing_plot_avoid_overlap_yticks=yes        #whether avoid overlap y-ticks(yes|no)
cphasing_plot_fontsize=auto                   #heatmap figure font size(auto|5|10)
cphasing_plot_dpi=300                         #plot figure dpi(150|300)
cphasing_low_memory=yes                       #reduce memory hyperpartition(yes|no)
##3D-DNA
3ddna_mapq=1,0                                #build map for a specific mapq(0|1)
3ddna_java_xms=50G                            #java initial heap size
3ddna_java_xmx=750G                           #java maximum heap size
3ddna_min_resolutions=5000                    #minimum resolutions(1000|5000|10000)
3ddna_clean_run_mode=no                       #clean up when done(yes|no)
##CondaEnv
cphasing_env_name=cphasing                    #C-Phasing env name
nextflow_env_name=nextflow                    #nextflow env name
conda_path=~/miniconda3                       #conda envs path
cphasing_path=~/software/CPhasing_v0.3.2      #C-Phasing software path
3ddna_path=~/software/3d-dna-201008           #3D-DNA software path

#######Run#######
1.1. deal with input data ...
[65/69749e] process > cphasing (deal_with) [100%] 1 of 1 ✔
Duration    : 35m 17s

Raw_reads   Raw_bases       Clean_reads  Clean_bases     Q20_rate  Q30_rate
75,947,702  11,344,186,400  75,947,702   11,344,186,400  98.977%   97.433%
1.2. copy hic cleandata ...
2 file(s) (  4.7 GiB) copied in  2m  1.8s ( 39.1 MiB/s).
2.1. build genome index ...
[c2/5e954a] process > index (minibwa) [100%] 3 of 3 ✔
Duration    : 31m 1s

2.2. align genome to Hi-C/Pore-C data ...
[68/c40504] process > align (bwa-mem2) [100%] 3 of 3 ✔
Duration    : 1h 12m 32s

2.3. retain high confidence regions to analysis ...
[74/19ec75] process > hcr (minibwa) [100%] 3 of 3 ✔
Duration    : 3m 36s

2.4. convert pairs to contacts ...
[b6/0b5961] process > convert_contacts (minibwa)  [100%] 3 of 3 ✔
Duration    : 1m 11s

3.1. running hyperpartition with【haploid】mode ...
[29/87cb29] process > hyperpartition (minibwa) [100%] 3 of 3 ✔
Duration    : 7m 56s

3.2. running scaffolding with【precision】method ...
[5a/705f46] process > scaffolding (bwa-mem2) [100%] 3 of 3 ✔
Duration    : 14m 41s

3.3. resort chromosomes by hic cool file ...
[03/3df570] process > resort_chr (_chromap) [100%] 3 of 3 ✔
Duration    : 6m 26s

4. generate heatmap figure ...
[2d/ebe68a] process > heatmap_plot (bwa-mem2) [100%] 3 of 3 ✔
Duration    : 6m 16s

5. 3d-dna generate .hic file for juicebox ...
[3f/755ced] process > juicebox (minibwa/q0) [100%] 6 of 6 ✔
Duration    : 42m 1s

#######Results#######
Output: ~/output_of_CPhasing-mod/
```
The Nextflow execution trace in the diagram has been hidden. For the specific time consumed by each process, please refer to the actual run .log file.    
⭐️The above tests were conducted on four nodes, each with 1TB of memory and 256 threads.

---

# Main output
The main output files are as follows:
```
.
├── cleandata
│   ├── HiC_R1.clean.fq.gz
│   ├── HiC_R2.clean.fq.gz
│   └── Reads_QC_stats.xls
├── juicebox
│   └── (haploid/phasing)
│       └── (used_pairs/used_bam/minibwa/bwa-mem2/chromap/...)
│           ├── heatmap
│           │   ├── original.heatmap.pdf(png/svg)
│           │   ├── use_hcr.sorted.heatmap.pdf(png/svg)
│           │   └── without_hcr.sorted.heatmap.pdf(png/svg)
│           ├── original.q*.hic                                 ⭐️ 1. Juicebox: File-->Open
│           ├── original.raw.assembly                           ⭐️ 2. Juicebox: Assembly-->Import Map Assembly
│           ├── use_hcr.review.assembly                         ⭐️ 3. Juicebox: Assembly-->Import Modified Assembly
│           └── without_hcr.review.assembly                     ⭐️ 3. Juicebox: Assembly-->Import Modified Assembly
└── stat
    └── Reads.stat.xls(txt)
```
