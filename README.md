### Project Title - Deploy a high-availability web app using CloudFormation
This is a cloud formation project that automates the creation of the infraestructure for deploying web applications. You can see the diagram Udacity.jpeg for visual reference.

This project contains two main YAML files:
    - Network: This template deploys a VPC, with a pair of public and private subnets spread 
    across two Availabilty Zones. It deploys an Internet Gateway, with a default 
    route on the public subnets. It deploys a pair of NAT Gateways (one in each AZ), 
    and default routes for them in the private subnets.

    The following parameters are mandatory:
        - EnvironmentName: name for the environment

    -Servers: This template deploys a Load Balancer with Launch Configuration, Auto Scalling Group and Security Groups.
    The Launch configuration fetches the web app from a s3 bucket and make it available via apache server.

    The following parameters are mandatory:
        - EnvironmentName: name for the environment
        - S3ZipResourceUrl: url for the s3 bucket from which the web app will be fetched. The url must mutch the pattern s3://<<bucket-name>>/<<resource>>.zip
        - S3ReadOnlyRole: role name for the s3 bucket read permissions. 

# Steps to deploy using default parameters files.
1. Create the s3 bucket and push the .zip file. This project provides a file named 'udagram.zip' that could be use as example. Then change the S3ZipResourceUrl with the s3 bucket url.
2. Create IAM Role for granting s3 bucket read permissions. Then change S3ReadOnlyRole property in server-parameters.json
3. Run ssh "sh create.sh "replace_with_your_infra_name" network.yml network-parameters.json"
4. Run ssh "sh create.sh "replace_with_your_server_name" servers.yml server-parameters.json"
5. Look for the HTTP-DNS-NAME output that will be generated from step 4 to test your web app !
