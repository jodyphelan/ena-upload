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

```bash
usage: ena-upload template [-h] -1 REGEX1 [-2 REGEX2] {single,paired}

positional arguments:
  {single,paired}       Single or paired end reads

options:
  -h, --help            show this help message and exit
  -1 REGEX1, --regex1 REGEX1
                        R1 regex pattern
  -2 REGEX2, --regex2 REGEX2
                        R2 regex pattern
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