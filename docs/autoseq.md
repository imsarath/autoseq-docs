## Getting Started

Autoseq is a command line tool and it has multiple pipelines used to analyse cancer genomics data from clinical samples. 

Piplines

 * Alascca
 * Liqbio *(UMI tag processing)*
 * RNAseq (under development)

*Latest version: [v0.6.0][dist]*

Note:

  **This version of autoseq is specially updated for PROBIO trail on prostate cancer.**

Installation
-------------

Step 1: Clone the alascca-dotfiles repo

```sh
git clone https://github.com/clinseq/probio-dotfiles.git /nfs/PROBIO/probio-dotfiles
```
Step 2: Go to dotfiles directory

```sh
cd /nfs/PROBIO/probio-dotfiles
```
Step 3: Run the `.bash_profile` file to create new environment

```sh
. /nfs/PROBIO/probio-dotfiles/.bash_profile
```

Step 4: Run this script to install all prerequisites

```sh
bash install-prereqs.sh
```

Command Line Usage
------------------

```sh
Usage: autoseq [OPTIONS] COMMAND [ARGS]...

Options:
  --ref TEXT          json with reference files to use
  --job-params TEXT   JSON file specifying various pipeline job parameters.
  --outdir PATH       output directory
  --libdir TEXT       directory to search for libraries
  --runner_name TEXT  Runner to use.
  --loglevel TEXT     level of logging
  --jobdb TEXT        sqlite3 database to write job info and stats
  --dot_file TEXT     write graph to dot file with this name
  --cores INTEGER     max number of cores to allow jobs to use
  --umi               To process the data with UMI- Unique Molecular
                      Identifier
  --scratch TEXT      scratch dir to use
  --help              Show this message and exit.

Commands:
  alascca
  liqbio
  liqbio-prepare

```

Generate the reference files
-----------------------------

`generate-ref` command can be used to generate all required reference files to run the pipeline. 

```sh
generate-ref --genome-resources /nfs/PROBIO/genome-resources --outdir /nfs/PROBIO/autoseq-genome
```



LiqBio Pipeline
---------------

```sh
autoseq --ref ref.json --outdir /path/to/outdir --jobdb jobdb.json --cores 5 --runner_name slurmrunner --libdir /path/to/libdir liqbio sample.json
```

*with UMI*

`--umi` flag is used to call UMI pipeline

```sh
autoseq --ref ref.json --outdir /path/to/outdir --jobdb jobdb.json --cores 5 --runner_name slurmrunner --libdir /path/to/libdir --umi liqbio sample.json
```

General Discriptions
--------------------

<b>Clinseq barcodes</b>

Each sample+preparation+capture item should have a corresponding barcode with the format `PROJECT-SDID-TYPE-SAMPLEID-PREPID-CAPTUREID` where:

* `PROJECT` is a two-letter short project designator. One of `AL` (alascca), `LB` (liquid biopspy) and `OT` (other)

* `SDID` is an identifier for a single individual. It must match the pattern `P-[a-zA-Z0-9]+` (*NOTE:* This necessitates an additional "-" within this field).

* `TYPE` is the sample type, one of `T` (tumor), `N` (normal) and `CFDNA` (ctDNA)

* `SAMPLEID` identifies a single biological sample, for example piece of a tumor or a single tube of plasma. It must match the pattern `[a-zA-Z0-9]+`.

* `PREPID` specifies the library preparation kit used. It must be a two-letter shortname followed by a string matching `[0-9]+`, which can be used to indicate the date on which the prep was performed. The date string should *preferably* be in the format `YYYYMMDDHHMM`. For example, `201701241540` would indicate year 2017, January 24th, at 15:40.

* `CAPTUREID` specifies the capture that was performed on the library (if any). It must match either `WGS` (indicating that no capture was performed), or else a two-letter shortname indicating the capture kit used, followed by a string matching `[0-9]+`, which can be used to indicate the date on which the capture was performed. The date should *preferably* be in the format `YYYYMMDDHHMM`.

*NOTE:* The combination `SDID-TYPE-SAMPLEID` must uniquely identify a single sample.

*NOTE:* A clinseq barcode is not garuanteed to uniquely specify a single sample+library+capture item, but in practice it should be unique if precise preparation and capture times are included within the `PREPID` and `CAPTUREID` fields.

<b>Allowed Prep IDs</b>

Autoseq know about the following preparation methods: 

* `BN` = `BIOO_NEXTFLEX`
* `KH` = `KAPA_HYPERPREP`
* `KP` = `KAPA_HYPERPLUS`
* `TD` = `THRUPLEX_DNASEQ`
* `TP` = `THRUPLEX_PLASMASEQ`
* `TF` = `THRUPLEX_FD`
* `TS` = `TRUSEQ_RNA`
* `NN` = `NEBNEXT_RNA`
* `VI` = `VILO_RNA`            

<b>Allowed Capture IDs</b>

Autoseq knows about the following capture kits:

* `CS` = `clinseq_v3_targets`
* `CZ` = `clinseq_v4`
* `EX` = `EXOMEV3`
* `EO` = `EXOMEV1`
* `RF` = `fusion_v1`
* `CC` = `core_design`
* `CD` = `discovery_coho`
* `CB` = `big_design`
* `TT` = `test-regions`
* `CM` = `monitor`
* `CP` = `progression`
* `PC` = `probio_comprehensive`
* `PB` = `probio_biomarker_signature`
* `PA` = `pancancer`

Newer version of autoseq has three more panels such as PC, PB and PA.

<b>Liqbio</b>

The `sample.json` file has the format (right side). In this file, a single tumor and normal sample is allowed, but multiple plasma samples. If no tumor or normal sample is avaialble, they can be set to `null`, but if no plasma samples are available, it should be set to `[]` (empty list), for example `"CFDNA": []`.

```
{
    "sdid": "NA12877",
    "panel": {
        "T": "NA12877-T-03098849-TD1-TT1",
        "N": "NA12877-N-03098121-TD1-TT1",
        "CFDNA": ["NA12877-CFDNA-03098850-TD1-TT1", "NA12877-CFDNA-03098850-TD2-TT1"]
    },
    "wgs": {
        "T": "NA12877-T-03098849-TD1-WGS",
        "N": "NA12877-N-03098121-TD1-WGS",
        "CFDNA": ["NA12877-CFDNA-03098850-TD1-WGS"]
    }
}
```

For the plasma samples, merging of libraries will take place before calling. On alignment, the `@RG` tag will be set as follows: 

* `ID` = `SDID-TYPE-SAMPLEID-PREPID-CAPTUREID`
* `LB` = `SDID-TYPE-SAMPLEID-PREPID`
* `SM` = `SDID-TYPE-SAMPLEID`

Of note is that the library tag (`LB`) does not include the `CAPTUREID` part, to ensure that PCR duplicates are removed correctly. 

If a single prepared samples is exposed to capture twice, to create the libraries `NA12877-T-49-TD1-TT1` and `NA12877-T-49-TD1-TT2` (note different digits in the capture id), read pairs being identical between the two libraries should be considered duplicates since the sample was split after the final PCR step. Therefore, the `LB` for these libraries is set to `NA12877-T-49-TD1`. After merging the bam files, removal of PCR duplicates is done using Picard MarkDuplicates, which will do the right thing. 
