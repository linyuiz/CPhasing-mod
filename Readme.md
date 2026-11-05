# Introduction（CPhasing）
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
⭐️ [**CPhasing-mod**](https://github.com/linyuiz/CPhasing-mod): Revised version of the genome scaffolding software [**C-Phasing**](https://wangyibin.github.io/CPhasing/).

⭐️ [**EDTA-mod**](https://github.com/linyuiz/EDTA-mod): Revised version of the TE annotation software [**EDTA**](https://github.com/oushujun/EDTA).

⭐️ [**GINGER-mod**](https://github.com/linyuiz/GINGER-mod): Revised version of the genome annotation software [**GINGER**](https://github.com/i10labtitech/GINGER).

---

# Installation
<p align="center"><strong>[ <a href="https://github.com/linyuiz/zgtools/wiki/English">English Wiki</a> | <a href="https://github.com/linyuiz/zgtools/wiki/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87">中文维基</a> ]</strong></p>
