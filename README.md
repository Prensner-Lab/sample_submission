# Sample submission guideline

When submitting data to the lab, please fill out [the data submission file](blob:https://github.com/905f952d-18ae-4372-acca-db676f0abf19) and send it to [clauwaer@umich.edu](mailto:clauwaer@umich.edu). Please keep the `.csv` file format after editing. as such, do not use comma’s within field entries.

This helper sheet provides additional information to fill out every field.

## Metadata

- **PI name**: Name of Principal Investigator of the lab
- **Date**: Date at which samples were created.
- **Submitter name**: Your name
- **Submitter email**: Your institution email
- **Project title:** Short title used as reference of the sample study
- **Project description**: Short description of the purpose of the study. Make sure to use a single line within the csv file.

## Table

Please fill in `NA` if field is not applicable. Additional columns can be added when missing.

- `run_id`: Current file name of the sample. Exclude the file extension and verify the ID is not a substring of another ID in the list.
- `smart_id`: determines downstream processing of the samples through several rules. Samples are supposed to share the same smart_id if:
  - They are meant to be merged, e.g. multiple runs.
  - They contain paired-end samples (e.g. R1 and R2; see field `read_end`)
  - They only differ from their data protocol (e.g. RNA_seq/Ribo_seq; see field `data_type`)

  Samples with identical smart_id’s are only merged if they have the same values in the `data_type` and `read_end` field. `smart_id` is furthermore used to identify samples in the result reports. As such, make sure the smart_id carries all identifying information relevant for identification within the project (e.g., control/replicate/dose/…)

  Example for RNA_seq:

  | **run_id** | **smart_id** |
  | --- | --- |
  | DIPG13_K27M_5Gy_1_S135_R1.fastq.gz | DIPG13_K27M_5Gy_1_S135 |
  | DIPG13_K27M_5Gy_1_S135_R2.fastq.gz | DIPG13_K27M_5Gy_1_S135 |
  | DIPG13_K27M_5Gy_2_S135_R1.fastq.gz | DIPG13_K27M_5Gy_2_S135 |
  | DIPG13_K27M_5Gy_2_S135_R2.fastq.gz | DIPG13_K27M_5Gy_2_S135 |

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
- `replicate_num`: Replicate number (integer)
- `is_paired_end`: Please use one of the following: true/false
- `read_end`: Please use on of the following: left/right/NA
- `experimental_type`: Please describe the experiment type. Could be one of the following: overexpression/knockdown/drug_treatment.
- `dose`: Dose of the administered drug
- `description`: Additional comments on the sample
