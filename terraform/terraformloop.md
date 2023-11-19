
**using count 
**
# Configure the AWS Provider
provider "aws" {
  region = "eu-west-3"
}

resource "aws_iam_user" "example" {
  count = length(var.user_names)
  name  = var.user_names[count.index]
}

variable "user_names" {
  description = "IAM usernames"
  type        = list(string)
  default     = ["user1", "user2", "user3"]
}





**
using for each**
# Configure the AWS Provider
provider "aws" {
  region = "eu-west-3"
}

resource "aws_iam_user" "example" {
  for_each = var.user_names
  name  = each.value
}

variable "user_names" {
  description = "IAM usernames"
  type        = set(string)
  default     = ["user1", "user2", "user3"]
}
