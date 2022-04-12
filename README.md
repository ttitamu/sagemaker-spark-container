# Custom SageMaker Spark Container

This repository has been forked from https://github.com/aws/sagemaker-spark-container. 
The goal of the custom spark container is to add custom Python packages to the image.

## Prerequisites

- install pipenv

```bash
pip install --user pipenv
```

- install pyenv
  - see https://www.liquidweb.com/kb/how-to-install-pyenv-on-ubuntu-18-04/

## How to build and push the custom image to ECR

The following instructions are modified from those in the DEVELOPMENT.md file.

1. set some environment variables.

```bash
export AWS_ACCOUNT_ID=<HTP account id>
export REGION=us-east-1
export SPARK_REPOSITORY=sagemaker-spark
export VERSION=latest
export SAGEMAKER_ROLE=<HTP publisher role>
```

2. build your image

```bash
make build
```

3. log into the ECR 

```bash
aws ecr get-login-password --region ${REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com
```

4. tag your image


```bash
docker tag ${SPARK_REPOSITORY}:latest ${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/${SPARK_REPOSITORY}:${VERSION}
```

5. push the latest image


```bash
docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${REGION}.amazonaws.com/${SPARK_REPOSITORY}:${VERSION}
```

## Spark Overview
Apache Spark™ is a unified analytics engine for large-scale data processing. It provides high-level APIs in Scala, Java, Python, and R, and an optimized engine that supports general computation graphs for data analysis. It also supports a rich set of higher-level tools including Spark SQL for SQL and DataFrames, MLlib for machine learning, GraphX for graph processing, and Structured Streaming for stream processing.

## SageMaker Spark Container
The SageMaker Spark Container is a Docker image used to run batch data processing workloads on Amazon SageMaker using the Apache Spark framework. The 
container images in this repository are used to build the pre-built container images that are used when running Spark jobs on Amazon SageMaker using the SageMaker Python SDK. The pre-built images are available in the Amazon Elastic Container Registry (Amazon ECR), and this repository serves as a reference for those wishing to build their own customized Spark containers for use in Amazon SageMaker.

For the list of available Spark images, see [Available SageMaker Spark Images](available_images.md).

## License
This project is licensed under the Apache-2.0 License.


## Usage in the SageMaker Python SDK

The simplest way to get started with the SageMaker Spark Container is to use the pre-built images via the SageMaker Python SDK.

[Amazon SageMaker Processing — sagemaker 2.5.3 documentation](https://sagemaker.readthedocs.io/en/stable/amazon_sagemaker_processing.html#amazon-sagemaker-processing)

## Getting Started With Development

To get started building and testing the SageMaker Spark container, you will have to setup a local development environment.

See instructions in [DEVELOPMENT.md](./DEVELOPMENT.md)

## Contributing
To contribute to this project, please read through [CONTRIBUTING.md](./CONTRIBUTING.md)

