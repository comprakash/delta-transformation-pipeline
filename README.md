# delta-transformation-pipeline
A transformation pipeline for Delta Lake

## Requirements
- Linux machine

## Setup
- Download Anaconda, Docker, MiniKube
- `conda create --name delta-transformation-pipeline python=3.10.11`
- `conda activate delta-transformation-pipeline`
- `conda install poetry`  
- `poetry install`
- `poetry self add poetry-dotenv-plugin`

## AWS Setup
```
aws dynamodb create-table \
  --region ap-south-1 \
  --table-name delta_log \
  --attribute-definitions AttributeName=tablePath,AttributeType=S \
                          AttributeName=fileName,AttributeType=S \
  --key-schema AttributeName=tablePath,KeyType=HASH \
               AttributeName=fileName,KeyType=RANGE \
  --billing-mode PAY_PER_REQUEST
```
```
aws dynamodb update-time-to-live \
  --region ap-south-1 \
  --table-name delta_log \
  --time-to-live-specification "Enabled=true, AttributeName=expireTime"
```