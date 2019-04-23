LiqBio 
======

*Non UMI pipeline*

1. **Preprocessing**
    * Trimming and Filtering
        * [skewer](https://github.com/relipmoc/skewer)
    * Mapping to Reference
        * [BWA](http://bio-bwa.sourceforge.net/bwa.shtml)
    * Indel Realignment
        * [GATK4](https://gatkforums.broadinstitute.org/gatk/discussion/7156/howto-perform-local-realignment-around-indels)
    * Merge Bams and Markdups
        * [Picard](https://broadinstitute.github.io/picard/)
2. **Germline Variant Calling**
    * SNV and small INDEL
        * [GATK4-HaplotypeCaller](https://software.broadinstitute.org/gatk/documentation/tooldocs/3.8-0/org_broadinstitute_gatk_tools_walkers_haplotypecaller_HaplotypeCaller.php)
        * [Strelka Germline](https://github.com/Illumina/strelka)
    * Combining Variants
        * [GATK3-CombineVariants](https://software.broadinstitute.org/gatk/documentation/tooldocs/3.8-0/org_broadinstitute_gatk_tools_walkers_variantutils_CombineVariants.php)
3. **Somatic Variant Calling**
    * SNV and small INDEL
        * [VarDict](https://github.com/AstraZeneca-NGS/VarDictJava)
        * [Strelka Somatic](https://github.com/Illumina/strelka)
        * [GATK4-Mutect2](https://gatkforums.broadinstitute.org/gatk/discussion/11136/how-to-call-somatic-mutations-using-gatk4-mutect2)
        * [Varscan](http://varscan.sourceforge.net/)
    * Combine and Filter Variants(Ensembl Approach)
        * [SomaticSeq](https://github.com/bioinform/somaticseq)
    * Annatotaion
        * [VeP-95](https://www.ensembl.org/info/docs/tools/vep/index.html)
4. **Structural Variant Calling**
    * SV - INS, INV, DEL, TRA, DUP
        * [svcaller - In-house developed](https://github.com/tomwhi/svcaller)
        * [svict](https://github.com/vpc-ccg/svict)
        * [Lumpy](https://github.com/arq5x/lumpy-sv)
        * [svaba](https://github.com/walaj/svaba)
5. **Copy Number Variation**
    * [CNVkit](https://cnvkit.readthedocs.io/en/stable/index.html)
    * [PureCN  in-house developed script](https://bioconductor.org/packages/devel/bioc/html/PureCN.html)
    * liqbio_CNA - for visualization
6. **QC Metrics**
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
    * Contamination Test
        * GATK conEst
    * MultiQC

*UMI pipeline*

1. UMI processing
    * Trimming and Filtering
        * [skewer](https://github.com/relipmoc/skewer)
    * Fastq to Bam
        * [fgbio-FastqToBam](http://fulcrumgenomics.github.io/fgbio/tools/latest/FastqToBam.html)
    * Alignment of Unmapped Bam - 1
        * [BWA](http://bio-bwa.sourceforge.net/bwa.shtml)
    * Realignment - 1
        * [GATK4](https://gatkforums.broadinstitute.org/gatk/discussion/7156/howto-perform-local-realignment-around-indels)
    * Group reads by umi
        * [fgbio-GroupReadsByUmi](http://fulcrumgenomics.github.io/fgbio/tools/latest/GroupReadsByUmi.html)
    * Call Duplex Consensus Reads
        * [CallDuplexConsensusReads](http://fulcrumgenomics.github.io/fgbio/tools/latest/CallDuplexConsensusReads.html)
    * Alignment - 2
        * [BWA](http://bio-bwa.sourceforge.net/bwa.shtml)
    * Realignment - 2
        * [GATK4](https://gatkforums.broadinstitute.org/gatk/discussion/7156/howto-perform-local-realignment-around-indels)
    * Filter Consensus Reads
        * [fgbio-FilterConsensusReads](http://fulcrumgenomics.github.io/fgbio/tools/latest/FilterConsensusReads.html)
    * Clip Overlapping Reads
        * [fgbio-ClipBam](http://fulcrumgenomics.github.io/fgbio/tools/latest/ClipBam.html)
    * Mark Duplicates (bam file from Realignment-1)
        * [Picard](https://broadinstitute.github.io/picard/)
2. Germline Variant Calling (bam file from clip overlapping bam)
    * SNV and small INDEL
        * [GATK4-HaplotypeCaller](https://software.broadinstitute.org/gatk/documentation/tooldocs/3.8-0/org_broadinstitute_gatk_tools_walkers_haplotypecaller_HaplotypeCaller.php)
        * [Strelka Germline](https://github.com/Illumina/strelka)
    * Combining Variants
        * [GATK3-CombineVariants](https://software.broadinstitute.org/gatk/documentation/tooldocs/3.8-0/org_broadinstitute_gatk_tools_walkers_variantutils_CombineVariants.php)
3. Somatic Variant Calling (bam file from clip overlapping bam)
    * SNV and small INDEL
        * [VarDict](https://github.com/AstraZeneca-NGS/VarDictJava)
        * [Strelka Somatic](https://github.com/Illumina/strelka)
        * [GATK4-Mutect2](https://gatkforums.broadinstitute.org/gatk/discussion/11136/how-to-call-somatic-mutations-using-gatk4-mutect2)
        * [Varscan](http://varscan.sourceforge.net/)
    * Combine and Filter Variants(Ensembl Approach)
        * [SomaticSeq](https://github.com/bioinform/somaticseq)
    * Annatotaion
        * [VeP-95](https://www.ensembl.org/info/docs/tools/vep/index.html)
4. Structural Variant Calling 
    * SV - INS, INV, DEL, TRA, DUP
        * [svcaller - In-house variant caller based on delly Algorythm](https://github.com/tomwhi/svcaller)
        * [svict](https://github.com/vpc-ccg/svict)
        * [Lumpy](https://github.com/arq5x/lumpy-sv)
        * [svaba](https://github.com/walaj/svaba)
5. Copy Number Variation
    * [CNVkit](https://cnvkit.readthedocs.io/en/stable/index.html)
    * [PureCN  in-house developed script](https://bioconductor.org/packages/devel/bioc/html/PureCN.html)
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
    * Contamination Test
        * GATK conEst
    * MultiQC

Alascca 
=======

*Alascca pipeline needs to be fixed as per new changes done in clinseq pipeline*