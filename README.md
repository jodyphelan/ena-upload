# ena-upload

## Description

This tool is used to upload files to the ENA (European Nucleotide Archive) using the FTP command line tool.

## Installation

```bash
# Install dependencies
pip install git+https://github.com/jodyphelan/fastq-files.git
# Install the package
pip install git+https://github.com/jodyphelan/ena-upload.git
```

## Usage

Uploading files to the ENA requires a Webin account. You can create an account [here](https://www.ebi.ac.uk/ena/submit/sra/#home).
1. Create a project to obtain a project accession (should start with PRJE).
2. Create a template file that can be populated in with the required metadata using the `ena-upload template` subcommand.
3. Populate the template file with the required metadata (including the project accession) and save it.
4. Upload the files to the ENA using the `ena-upload upload` subcommand. This will split the template file into two files, one for the samples and one for the runs. 
5. Manually upload the sample and run files to the ENA and the submission will be created.

### Subcommands help
```bash
usage: ena-upload [-h] [--version] {template,upload} ...

ENA Uploader

positional arguments:
  {template,upload}  sub-command help
    template         Discover fastq files and create a template file
    upload           Upload fastq files to ENA

options:
  -h, --help         show this help message and exit
  --version          show program's version number and exit
```

### Template help

This step will find fastq files and create a template file that can be filled in with the required metadata.

You can do this either by providing a regex pattern for the R1 and R2 files or by providing a list of files. 

```bash
usage: ena-upload template [-h] {regex,file} ...

positional arguments:
  {regex,file}  sub-command help
    regex       Use regex to find single end fastq files
    file        Use a file to find fastq files

options:
  -h, --help    show this help message and exit
```
#### Template Regex help

This step will find fastq files using a regex pattern and create a template file that can be filled in with the required metadata.

```bash
usage: ena-upload template regex [-h] -1 REGEX1 [-2 REGEX2]

options:
  -h, --help            show this help message and exit
  -1 REGEX1, --regex1 REGEX1
                        R1 regex pattern
  -2 REGEX2, --regex2 REGEX2
                        R2 regex pattern
```

#### Template File help

This step will find fastq files using a list of files and create a template file that can be filled in with the required metadata.
The file should be a TSV file with required columns `ID` and `R1`, and optional column `R2`.

```bash
usage: ena-upload template file [-h] file

positional arguments:
  file        TSV file with required columns `ID` and `R1`, and optional column `R2`

options:
  -h, --help  show this help message and exit
```

### Upload help

This step will upload the fastq files to the ENA and split the template file into two files, one for the samples 
and one for the runs. The files will be can then be manually uploaded to the ENA and the submission will be created.

```bash
usage: ena-upload upload [-h] template username password

positional arguments:
  template    Filled in template file
  username    Webin username
  password    Webin password

options:
  -h, --help  show this help message and exit
```