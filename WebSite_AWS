# terraform/website/aws

provider "aws" {
  access_key = ""
  secret_key = ""
  region     = ""
}

resource "aws_instance" "for_terraform" {
  ami                    = ""  # Amazon Linux AMI
  instance_type          = "t2.micro"
  vpc_security_group_ids = [aws_security_group.for_terraform.id]
  user_data              = <<EOF
#!bin/bash
yum -y update
yum -y install httpd
myip= 'curl http://169.254.169.254/latest/meta-data/local-ipv4'
echo "<h2>WebServer with IP :$myip</h2><br>Build by Terraform!" > /var/www/html/index.html
sudo service httpd start
chkconfig httpd on
EOF
}

resource "aws_security_group" "for_terraform" {
  name        = "for_terraform security group"
  description = "My First SecurityGroup"

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }
  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "For_Terraform"
  }
}
