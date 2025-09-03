# cloud--computing--labs
My cloud computing learning journey with projects labs for AWS, Azure and GCP

s3-static-website/
│
├── main.tf
├── variables.tf
├── outputs.tf
├── index.html
├── error.html
└── README.md

Teraform code 
main.tf
provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "static_site" {
  bucket = var.bucket_name
  acl    = "public-read"

  website {
    index_document = "index.html"
    error_document = "error.html"
  }
}

resource "aws_s3_bucket_object" "index" {
  bucket = aws_s3_bucket.static_site.bucket
  key    = "index.html"
  source = "index.html"
  acl    = "public-read"
  content_type = "text/html"
}

resource "aws_s3_bucket_object" "error" {
  bucket = aws_s3_bucket.static_site.bucket
  key    = "error.html"
  source = "error.html"
  acl    = "public-read"
  content_type = "text/html"
}

output "website_url" {
  value = aws_s3_bucket.static_site.website_endpoint
}


variable.tf
variable "bucket_name" {
  description = "The name of the S3 bucket"
  type        = string
}


output.tf
output "bucket_name" {
  value = var.bucket_name
}

index.html
<!DOCTYPE html>
<html>
<head>
  <title>My Static Site</title>
</head>
<body>
  <h1>Hello from the Cloud! 🚀</h1>
</body>
</html>


erroe.html
<!DOCTYPE html>
<html>
<head>
  <title>Error</title>
</head>
<body>
  <h1>Oops! Something went wrong.</h1>
</body>
</html>



