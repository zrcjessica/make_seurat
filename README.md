# make_seurat

This pipeline runs [cellranger-count](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/count) with a custom reference genome on FASTQ files for scRNA-seq experiments and generates Seurat objects (`.rds`) from the resulting count data with corresponding QC plots. 

This pipeline was designed for analyzing snRNA-seq from outbred rats classified by addiction index following self-administration of oxycodone or cocaine, in addition to rats that were never exposed to any drug (naive). 

## Usage
To run this pipeline, fill out the fields in the config file (`config.yml`) with your respective paths to the specified files and directories. 

### `config.yml` 

#### `out`
Specify the relative path to the directory where output files will be written

#### `data`
Specify path where you want outputs of `cellranger count` to be written - can specify the same directory as `out`

#### `fastqs_ref`
This specifies a .tsv file with four columns:
| RFID                              | Treatment                      | Addiction index      | FASTQ prefix                                      |
|-----------------------------------|--------------------------------|----------------------|---------------------------------------------------|
| Should correspond to sample names | e.g. cocaine, oxycodone, naive | e.g. high, low, none | Sample prefix for all FASTQ files for this sample; see [10x docs] for details](https://support.10xgenomics.com/single-cell-gene-expression/software/pipelines/latest/using/fastq-input) |

#### `fastqs_dir`
Path to directory containing subdirectories each named after a sample (RFID). Each subdirectory contains all the FASTQ files for each sample. 

e.g. 
```bash
├── 933000120138414
│   ├── A_HS_2_JB_168_1_S41_L002_R1_001.fastq.gz
│   ├── A_HS_2_JB_168_1_S41_L002_R2_001.fastq.gz
│   ├── A_HS_2_JB_168_2_S42_L002_R1_001.fastq.gz
│   ├── A_HS_2_JB_168_2_S42_L002_R2_001.fastq.gz
│   ├── A_HS_2_JB_168_3_S43_L002_R1_001.fastq.gz
│   ├── A_HS_2_JB_168_3_S43_L002_R2_001.fastq.gz
│   ├── A_HS_2_JB_168_4_S44_L002_R1_001.fastq.gz
│   ├── A_HS_2_JB_168_4_S44_L002_R2_001.fastq.gz
│   ├── Rat_Opioid_HS_2_S2_L001_R1_001.fastq.gz
│   └── Rat_Opioid_HS_2_S2_L001_R2_001.fastq.gz
├── 933000120138586
│   ├── A_933000120138586_JB_246_S4_L002_R1_001.fastq.gz
│   └── A_933000120138586_JB_246_S4_L002_R2_001.fastq.gz
├── 933000120138592
│   ├── A_933000120138592_JB_245_S3_L002_R1_001.fastq.gz
│   └── A_933000120138592_JB_245_S3_L002_R2_001.fastq.gz
```


