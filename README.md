# terraform-aws-module-s3-bucket
Terraform s3 bucket with AES256 enabled and private bucket enabled


## Usage
```hcl

provider "aws" {
  profile   = "profile"
  region    = "ap-southeast-1"
}

resource "aws_s3_bucket" "mybucket" {
  bucket = "mybucket-tfcourse-05222020"
  acl    = "private"
  region = "ap-southeast-1"

  server_side_encryption_configuration {
    rule {
      apply_server_side_encryption_by_default {
        sse_algorithm     = "AES256"
      }
    }
  }

  tags = {
   Owner = "Test"
   }
}

resource "aws_s3_bucket_public_access_block" "mybucket1" {
  bucket = aws_s3_bucket.mybucket.id

  block_public_acls   = true
  block_public_policy = true
  ignore_public_acls = true
  restrict_public_buckets = true
}
```
