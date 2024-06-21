# Sample submission guideline

When submitting data to the lab, please fill out [the data submission file](https://github.com/Prensner-Lab/sample_submission/blob/main/sample_submission_prensner_lab.csv), rename it to properly reflect the project, and send it to [clauwaer@umich.edu](mailto:clauwaer@umich.edu). When using Excel, please save as a `.csv` file format after editing. as such, refrain from using comma’s within field entries.

This documentation provides additional information to fill out every field.

## Metadata

- **PI name**: Name of Principal Investigator of the lab
- **Date**: Date at which samples were created.
- **Submitter name**: Your name
- **Submitter email**: Your institution email
- **Project title:** Short title used as reference of the sample study
- **Project description**: Short description of the purpose of the study. Make sure to use a single field within the csv file.

## Table

Please fill in `NA` if field is not applicable. Additional columns can be added when missing.

- `run_id`: File name of the sample. Include the file extension.
- `smart_id`: ID used for downstream processing of the samples. Furthermore, this `smart_id` links samples through several rules. Samples are supposed to share the same `smart_id` if:
  - They are meant to be merged (reads are combined), e.g. multiple technical replicates run for greater read depth. Don't use the same `smart_id` for biological replicates!
  - They are paired-end samples (e.g. R1 and R2; see field `read_end`)
  - They only differ from their data protocol (e.g. RNA_seq/Ribo_seq; see field `data_type`)

  Samples with identical smart_id’s are only merged if they have the same values in the `data_type` and `read_end` field. `smart_id` is furthermore used to identify samples in the result reports. As such, include essential information relevant for identification of the sample (e.g., control/replicate/dose/…) while excluding any of the nondescript or redundant info present within the original `run_id` of the sample. 

  Example for RNA_seq data featuring two biological replicates:

  | **run_id** | **smart_id** | **data_type** | **read_end** |
  | --- | --- | --- | --- |
  | 123_0313_R1.fastq.gz | DIPG13_K27M_5Gy_1 | RNA_seq | R1 |
  | 123_0314_R2.fastq.gz | DIPG13_K27M_5Gy_1 | RNA_seq | R2 |
  | 123_0315_R1.fastq.gz | DIPG13_K27M_5Gy_2 | RNA_seq | R1 |
  | 123_0316_R2.fastq.gz | DIPG13_K27M_5Gy_2 | RNA_seq | R2 |

- `data_type`: Please use one of the following terms:
  - RNA_seq
  - Ribo_seq
  - Disome_seq
  - ChIP_seq
  - Exome_seq
  - Whole_genome_seq
  - Other (detail further in description)
- `species`: Species identifier
- `type`: Please use one of the following: autopsy/tissue_sample/cell_line
- `source_id`: Cell line code, patient ID or other unique identifiers.
- `control_experimental`: Please use one of the following: control/experimental
- `replicate_num`: Biological replicate number (integer)
- `is_paired_end`: Please use one of the following: true/false
- `read_end`: Please use on of the following: R1/R2/NA
- `experimental_type`: Please describe the experiment type. Could be one of the following: overexpression/knockdown/drug_treatment.
- `dose`: Dose of the administered drug
- `sequencing_instrument`: sequencing instrument on which the samples were run on
- `description`: Additional comments on the sample
