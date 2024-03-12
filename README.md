# ![nf-core/awsomicstest]

## Introduction

**nf-core/awsomicstest** is a bioinformatics pipeline that simply tests the functionality of a nf-core based workflow in AWS HealthOMICS.


## Usage

This workflow can be installed and setup by following this procedure:

**1. Setup ECR** Deploy the ecr helper from here: [https://github.com/aws-samples/amazon-ecr-helper-for-aws-healthomics](https://github.com/aws-samples/amazon-ecr-helper-for-aws-healthomics).
Once deployed using the following command and supply the [container_image_manifest.json](https://raw.githubusercontent.com/wslh-bio/nf-core-awsomicstest/main/container_image_manifest.json) included in this repository:

```
aws stepfunctions start-execution \
    --state-machine-arn arn:aws:states:<aws-region>:<aws-account-id>:stateMachine:omx-container-puller \
    --input file://container_image_manifest.json
```

**2. Upload nf-core-awsomicstest workflow** Upload the [nf-core-awsomicstest.zip](https://github.com/wslh-bio/nf-core-awsomicstest/releases) from the release into an S3 bucket accessible by AWS Health OMICS.

**3. Setup the workflow** in AWS using the aws management console, at the parameters step use the [parameter-template.json](https://raw.githubusercontent.com/wslh-bio/nf-core-awsomicstest/main/parameter-template.json) to configure the parameters.

**4. Build the Samplesheet** The sample sheet needs to be `csv` format and have three headers and point to where the data is located in S3. Here is example:

|sample|fastq_1|fastq_2|
|---|---|---|
|TestSample01|s3://\<bucket-name\>/\<prefix-name\>/TestSample01_R1.fastq.gz|s3://\<bucket-name\>/\<prefix-name\>/TestSample01_R2.fastq.gz|


Now, you can run the pipeline in AWS Health Omics!

## Credits

nf-core/awsomicstest was originally written by CJ Jossart.
