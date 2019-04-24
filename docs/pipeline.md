Alascca 
=======
 
The worflow is descriped below with tools as used.

1. Preprocessing
    * Trimming and Filtering
        * [skewer](https://github.com/relipmoc/skewer)
    * Mapping to Reference
        * [BWA](http://bio-bwa.sourceforge.net/bwa.shtml)
    * Merge Bams and Markdups
        * [Picard](https://broadinstitute.github.io/picard/)
2. Germline Variant Calling
    * SNV and small INDEL
        * [FreeBayes](https://github.com/ekg/freebayes)
    * VCF add Sample-Tumor
3. Somatic Variant Calling
    * SNV and small INDEL
        * [VarDict](https://github.com/AstraZeneca-NGS/VarDictJava)
    * Annatotaion
        * [VeP](https://www.ensembl.org/info/docs/tools/vep/index.html)
4. Copy Number Variation
    * [CNVkit](https://cnvkit.readthedocs.io/en/stable/index.html)
      * ALASCCA CNA - Tumor
5. QC Metrics
    * Fastq - Quality Check
        * [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
    * Coverage
        * alascca coverage hist
        * coverage qc call
    * hsmetrics
        * [Picard](https://broadinstitute.github.io/picard/)
    * OXOG metrics
        * [Picard](https://broadinstitute.github.io/picard/)
    * Insert size 
        * [Picard](https://broadinstitute.github.io/picard/)
    * Sequencing Depth 
        * sambamba-depth
    * MSI
        * [msisensor](https://github.com/ding-lab/msisensor)
    * Heterozygous Concordance 
        * [hz-concordance Tool]()
    * Contamination Test
        * GATK conEst
    * MultiQC
6. Alascca Report
    * compile Metadata and Genomic data
    * Generate report


LiqBio
======

1. Preprocessing
    * Trimming and Filtering
        * [skewer](https://github.com/relipmoc/skewer)
    * Mapping to Reference
        * [BWA](http://bio-bwa.sourceforge.net/bwa.shtml)
    * Merge Bams and Markdups
        * [Picard](https://broadinstitute.github.io/picard/)
2. Germline Variant Calling
    * SNV and small INDEL
        * [FreeBayes](https://github.com/ekg/freebayes)
    * VCF add Sample-Tumor
3. Somatic Variant Calling
    * SNV and small INDEL
        * [VarDict](https://github.com/AstraZeneca-NGS/VarDictJava)
    * Annatotaion
        * [VeP](https://www.ensembl.org/info/docs/tools/vep/index.html)
4. Structural Variant Calling
    * SV - INS, INV, DEL, TRA, DUP
        * [svcaller]()
5. Copy Number Variation
    * [CNVkit](https://cnvkit.readthedocs.io/en/stable/index.html)
    * [PureCN]()
    * liqbio_CNA - for visualization
6. QC Metrics
    * Fastq - Quality Check
        * [FastQC](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
    * Coverage
        * alascca coverage hist
        * coverage qc call
    * hsmetrics
        * [Picard](https://broadinstitute.github.io/picard/)
    * OXOG metrics
        * [Picard](https://broadinstitute.github.io/picard/)
    * Insert size 
        * [Picard](https://broadinstitute.github.io/picard/)
    * Sequencing Depth 
        * sambamba-depth
    * MSI
        * [msisensor](https://github.com/ding-lab/msisensor)
        * [mSINGS](https://bitbucket.org/uwlabmed/msings/src/master/) - Tumor only
    * Heterozygous Concordance 
        * [hz-concordance Tool]()
    * Contamination Test
        * GATK conEst
    * MultiQC




