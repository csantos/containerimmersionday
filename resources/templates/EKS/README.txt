EKS Cluster Stack Instructions:

1- Create an s3 bucket and upload the archive.zip and eks_lab_cloud9.yaml files to the bucket.
2- Make the bucket available to your account to be able to read the files within imageType
3- update the eks-base.yml file (Line 10 with the name of the s3 bucket you created)
4- Run the eks-base.yml file as a cloudformation script


The eks-base.yml will trigger Code Build to build the EKS Cluster
Please note: Using Code Build will incur costs

The Stack will also create a cloud9 instance as per the workshop instructions
