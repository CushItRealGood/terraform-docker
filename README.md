# Docker via Terraform and AWS
### ADD DESCRIPTION HERE 24hour time period after account creation to access ec2 dashboard and create key pair
1. Create AWS account
2. [Create IAM user](https://console.aws.amazon.com/iam/home)
   - Select Programmatic access for access type
   - Give the user 'AdministratorAccess' policy or create a Admin group with 'AdministratorAccess' and add that user to it.
   - After creating the user you will get the access key ID and secret access key. You will need these for our secret.tfvars file.
3. [Create a key pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) called ec2keys and save ec2keys.pem to this project location
4. Clone Repo and run terraform init
   ```
   git clone https://github.com/CushItRealGood/terraform-docker.git
   cd ./terraform-docker
   terraform init
   ```
5. Edit and rename secret.tfvars.example to secret.tfvars, input your IAM user key and secret and run the following:
   ```
   terraform plan -var-file='secret.tfvars'
   terraform apply -var-file='secret.tfvars' -auto-approve
   ```
6. Log into AWS by using the output value of 'aws_instance_public_dns'
   ```
   ssh -i <key location> admin@<ec2 public dns entry>
   example:
   ssh -i ec2keys.pem admin@ec2-52-234-127-217.compute-1.amazonaws.com
   ```
   
## Reference Materials:
 - Reviewed this [blog](https://blog.codeship.com/terraforming-your-docker-environment-on-aws/) by Phillip Shipley
 - Also watched some of Ned Bellavance [Getting Started with Terraform](https://app.pluralsight.com/library/courses/terraform-getting-started) on Pluralsite
