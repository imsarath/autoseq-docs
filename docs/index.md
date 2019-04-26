##Autoseq: A clinical genomics workflow management platform to analyze next generation sequencing data from cancer samples.


Autoseq system consists of different pipelines that can be used to analyze clinical genomics data generated on Illumina platform. Autoseq pipelines take raw sequencing data (fastq) as input and give an actionable variant report as output (pdf). Alascca and Liqbio are the predominant pipelines used to analyse targeted resequencing data.

Alascca pipeline was designed primarily to analyse data from the ALASCCA study which is a randomized, placebo-controlled, multicenter study of the value of low dose aspirin (ASA) added to patients with colorectal cancer.

LiqBio pipeline is used to analyze cell free DNA from blood samples in PROBIO study, Prostate cancer. Liqbio pipeline has two versions, one with regular data analysis steps and another pipeline with additional umi processing steps.

Autoseq's entire platform along with utility scripts are written in Python 2.7 and Python 3.6. We are currently porting all versions of the code to Python 3.6 for harmonious functioning of the pipelines.


| Source code | [GitHub](https://github.com/ClinSeq/autoseq)|
|-------------|-----------------------------------------------|
| <b>License</b> | [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)|
| <b>Packages</b> | [Python 2.7]() | [Conda Package Management](https://docs.conda.io/en/latest/)|
| <b>Q&A</b> | [Questions & Answers](https://github.com/ClinSeq/autoseq)|


* [Quick Start](autoseq/)

    * [Getting Started](autoseq/#getting-started)
    * [Installation](autoseq/#installation)
    * [Command Line usage](autoseq/#command-line-usage)
    * [General Discriptions](autoseq/#general-discriptions)

###CLI Options 

  * Pipelines
      * alascca
      * liqbio 

  * Tool
      * autoseq
      * generate_ref




