# Sample submission guideline

# NOTE: REFER TO (https://docs.google.com/spreadsheets/d/12ghgV_agYnepJ4B8aMvt7RLX8n6RFVRz4j3CEHhFIAU/edit?usp=sharing)[https://docs.google.com/spreadsheets/d/12ghgV_agYnepJ4B8aMvt7RLX8n6RFVRz4j3CEHhFIAU/edit?usp=sharing] INSTEAD FOR SAMPLE SHEET SUBMISSION
When submitting data to the lab, please fill out [the data submission file](https://raw.githubusercontent.com/Prensner-Lab/sample_submission/main/YYYYMMDD_%3Cproject_id%3E_sample_sheet.csv), rename it to properly reflect the project, and send it to [clauwaer@umich.edu](mailto:clauwaer@umich.edu).

Some notes:
  - When using Excel, please save as a `.csv` file format after editing. The file is parsed by our pipelines and therefore needs to be in a [flat file format](https://en.wikipedia.org/wiki/Flat-file_database).
  - Refrain from using comma’s within field entries.
  - Use the underscore character ('_') instead of spaces in the main Table (not the Metadata section).

When renaming the sample submission sheet, follow the naming convention `YYYYMMDD_<project_id>_sample_sheet.csv`. Where the project ID reflects the experimental setup of the data (e.g., `20240615_MS_MBL_MYC_groups_sample_sheet.csv`, `20220927_A673_bromo_menin_inhibitor_treatment_sample_sheet.csv`.

This documentation provides additional information to fill out every field.

## Metadata

- **PI name**: Name of Principal Investigator of the lab
- **Date**: Date at which samples were created. **Use YYYYMMDD format** (don't use additional '/' or '-').
- **Submitter name**: Your name
- **Submitter email**: Your institution email
- **Project title:** Short title used as reference of the sample study
- **Project description**: Short description of the purpose of the study. Make sure to use a single field within the csv file.

## Table

Please fill in `NA` if field is not applicable. Additional columns can be added when missing.

- `run_id`: File name of the data generated from the sample. Include the file extension. **Leave empty or use sample reference if filling out before data is processed**
- `smart_id`: ID used for downstream processing of the samples. **Make sure this value is intelligible and differentiates samples from each other that are not supposed to be merged, as this `smart_id` is used in all the report files**. Use properties essential to the experimental set-up (E.g., KO vs. Control, Dose rates, replicate number). An example for RNA_seq data featuring two biological replicates:

  | **run_id** | **smart_id** | **data_type** | **read_end** | **replicate_num** |  **treatment_id** |
  | --- | --- | --- | --- | --- | --- |
  | 123_0313_R1.fastq.gz | DIPG13_K27M_5Gy_1 | RNA_seq | R1 | 1 | 5Gy |
  | 123_0313_R2.fastq.gz | DIPG13_K27M_5Gy_1 | RNA_seq | R2 | 1 | 5Gy |
  | 123_0314_R1.fastq.gz | DIPG13_K27M_5Gy_2 | RNA_seq | R1 | 2 | 5Gy |
  | 123_0314_R2.fastq.gz | DIPG13_K27M_5Gy_2 | RNA_seq | R2 | 2 | 5Gy |
  | 123_0315_R1.fastq.gz | DIPG13_K27M_10Gy_1 | RNA_seq | R1 | 1 | 10Gy |
  | 123_0315_R2.fastq.gz | DIPG13_K27M_10Gy_1 | RNA_seq | R2 | 1 | 10Gy |
  | 123_0316_R1.fastq.gz | DIPG13_K27M_10Gy_2 | RNA_seq | R1 | 2 | 10Gy |
  | 123_0316_R2.fastq.gz | DIPG13_K27M_10Gy_2 | RNA_seq | R2 | 2 | 10Gy |

  This `smart_id` links samples through several rules. Samples are supposed to share the same `smart_id` when:
  - They are paired-end samples (e.g. R1 and R2; see field `read_end` and above example)
  - They only differ from their data protocol (e.g. RNA_seq/Ribo_seq; see field `data_type`)
  - They are meant to be merged (reads are combined), e.g. multiple technical replicates run for greater read depth. Don't use the same `smart_id` for biological replicates!

  Samples are only merged if they have identical `smart_id`s and also have the same values in the `data_type` and `read_end` field. 

- `data_type`: Please use one of the following values:
  - RNA_seq
  - Ribo_seq
  - ONTRNA_seq
  - Disome_seq
  - ChIP_seq
  - Exome_seq
  - WGS
  - Other (detail further in description)
- `species`: Species identifier
- `sample_type`: Please use one of the following: autopsy/tissue_sample/cell_line
- `source_id`: Cell line code, patient ID or other unique identifiers.
- `is_paired_end`: Please use one of the following: true/false
- `read_end`: Please use on of the following: R1/R2/NA
- `experiment_type`: Could be one of the following: overexpression/knockdown/drug_treatment.
- `test_or_control`: Used by the differential expression pipeline to understand which sample is the reference. Use either `test` or `control`.
- `location_id`
- `disease_id`
- `treatment_id`: Use a short string to denote one or multiple treatment groups, such as the amount of administered drug and/or the gene that is knocked out/overexpressed (e.g. `K27M_noIR`, `K27M_5Gy`, `K27M_10Gy`, `KO_noIR`, `KO_5Gy`, `KO_10Gy`). In other cases, for large sample cohorts, it might be more applicable to use sample types (e.g., Cancer type `MBL_group_3`, `MBL_group_2`, etc.). Treatment ID's determine how samples are grouped for differential expression analysis, where each group of samples is compared against all other groups. Replicates should be grouped together (i.e. sharing the same treatment ID).
- `replicate_num`: Biological replicate number (integer)
- `sequencing_instrument`: sequencing instrument on which the samples were run on
- `batch_date`: date of processing. **Use YYYYMMDD format** (don't use additional '/' or '-'). Can be different when project data is retrieved over multiple batches. Or when Ribo-seq and RNA-seq are processed at different dates.
- `description`: Free from description of the sample. Can be used for more comments on the treatment etc.
- Custom columns can be added for referencing information that is relevant.
