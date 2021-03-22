# iac-github-backup-kubernetes
GitHub Backup utils can be downloaded from https://github.com/github/backup-utils and the requirement was to keep the app inside a container. There is a no container image build by GitHub but it have Docker https://github.com/github/backup-utils/blob/master/Dockerfile file to create image we have include aws cli utility as per our requirement to push backup to S3 using aws cli. sample Docker file is Docker-AWS.

Build container images
We have build container images, and uploaded to Amazon ECR.

 Clone upstream Git repository


    $ mkdir devel
    $ cd devel
    $ git clone https://github.com/github/backup-utils.git
    $ cd backup-utils


Build container image and push it to ECR

    $docker build -t github-backup-utils-aws
    
Note :- Before pushing image into ECR you have to setup registry into ECR. 

Explanation:

Created namespace 

    $ kubectl apply -f ns.yaml
  
Edit below files and change values as per environment 
    
    1. "S3_upload" and change "S3_BUCKET" as per environment
    2. "back-config-example"
    3. "known-hosts-configmap.yaml"
    4. "private-key-secret.yaml"
   
