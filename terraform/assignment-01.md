
resource "aws_vpc" "vpc" {
  cidr_block = "10.0.0.0/16"
  enable_dns_support = true
  enable_dns_hostnames = true
  tags = {
    Name = "ninja-vpc-01"
  }
}

resource "aws_subnet" "pub_sub_01" {
  vpc_id                  = aws_vpc.ninja_vpc.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "eu-west-3a"
  map_public_ip_on_launch = true
  tags = {
    Name = "ninja-pub-sub-01"
  }
}

resource "aws_subnet" "pub_sub_02" {
  vpc_id                  = aws_vpc.ninja_vpc.id
  cidr_block              = "10.0.2.0/24"
  availability_zone       = "eu-west-3b"
  map_public_ip_on_launch = true
  tags = {
    Name = "ninja-pub-sub-02"
  }
}


resource "aws_subnet" "pri_sub_01" {
  vpc_id                  = aws_vpc.ninja_vpc.id
  cidr_block              = "10.0.3.0/24"
  availability_zone       = "eu-west-3a"
  tags = {
    Name = "ninja-priv-sub-01"
  }
}
resource "aws_subnet" "pri_sub_02" {
  vpc_id                  = aws_vpc.ninja_vpc.id
  cidr_block              = "10.0.4.0/24"
  availability_zone       = "eu-west-3b"
  tags = {
    Name = "ninja-priv-sub-02"
  }
}

resource "aws_key_pair" "key-pair-01" {
key_name = "ninja-01"
public_key = tls_private_key.rsa.public_key_openssh
}
resource "tls_private_key" "rsa" {
algorithm = "RSA"
rsa_bits  = 4096
}
resource "local_file" "key-01" {
content  = tls_private_key.rsa.private_key_pem
file_permission = "0400"
filename = "ninja-01.pem"
}


resource "aws_instance" "bastion_instance" {
  ami           = "ami-00983e8a26e4c9bd9" 
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.ninja_pub_subnet_01.id
  key_name      = "ninja-01"  
  tags = {
    Name = "bastion-instance"
  }
}
resource "aws_instance" "private_instance" {
  ami           = "ami-00983e8a26e4c9bd9"  
  instance_type = "t2.micro"
  subnet_id     = aws_subnet.ninja_priv_subnet_01.id
  key_name      = "ninja-01" 
  tags = {
    Name = "private-instance"
  }
}

resource "aws_internet_gateway" "ninja_igw" {
  vpc_id = aws_vpc.ninja_vpc.id
  tags = {
    Name = "ninja-igw-01"
  }
}

resource "aws_eip" "elastic_ip" {
  domain           = "vpc"
  # network_interface = aws_vpc.ninja_vpc.id
  #  depends_on = aws_internet_gateway.ninja_ig
}

resource "aws_nat_gateway" "ninja_nat" {
  allocation_id = aws_eip.elastic_ip.id
  subnet_id     = aws_subnet.ninja_pub_subnet_01.id
  tags = {
    Name = "ninja-nat-01"
  }
}

resource "aws_route_table" "ninja_route_pub" {
  vpc_id = aws_vpc.ninja_vpc.id
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.ninja_igw.id
  }
  tags = {
    Name = "ninja-route-pub-01"
  }
}

resource "aws_route_table_association" "public_route_association01" {
  subnet_id      = aws_subnet.ninja_pub_subnet_01.id
  route_table_id = aws_route_table.ninja_route_pub.id
}
resource "aws_route_table_association" "public_route_association02" {
  subnet_id      = aws_subnet.ninja_pub_subnet_02.id
  route_table_id = aws_route_table.ninja_route_pub.id
}

resource "aws_route_table" "ninja_route_priv" {
  vpc_id = aws_vpc.ninja_vpc.id
  route {
    cidr_block = "0.0.0.0/0"
    nat_gateway_id = aws_nat_gateway.ninja_nat.id
  }
  tags = {
    Name = "ninja-route-priv-01"
  }
}

resource "aws_route_table_association" "private_route_association01" {
  subnet_id      = aws_subnet.ninja_priv_subnet_01.id
  route_table_id = aws_route_table.ninja_route_priv.id
}

resource "aws_route_table_association" "private_route_association02" {
  subnet_id      = aws_subnet.ninja_priv_subnet_02.id
  route_table_id = aws_route_table.ninja_route_priv.id
}


