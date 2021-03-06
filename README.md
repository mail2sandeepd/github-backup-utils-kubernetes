# github-backup-utils-kubernetes
GitHub Backup utils can be downloaded from https://github.com/github/backup-utils and the requirement was to keep the app inside a container. There is a no container image build by GitHub but it have Docker https://github.com/github/backup-utils/blob/master/Dockerfile file to create image we have include aws cli utility as per our requirement to push backup to S3 using aws cli. sample Docker file is https://github.com/mail2sandeepd/github-backup-utils-kubernetes/blob/main/Docker-AWS.

Build container images
We have build container images, and uploaded to Amazon ECR.

 Clone upstream Git repository


    $ mkdir work
    $ cd work
    $ git clone https://github.com/github/backup-utils.git
    $ cd backup-utils


Build container image and push it to ECR

    $docker build -t github-backup-utils-aws
    
Note :- Before pushing image into ECR you have to setup registry into ECR. 

Explanation:

Converted private key into secret and create secret from this

    $kubectl create secret generic --from-file=private_key_file -o yaml --dry-run=client > private-key-secret.yaml

Deploying kubernetes job for backup and pushing backup to AWS S3.

    $ kubectl apply -f ns.yaml
    $ kubectl apply -f private-key-secret.yaml
    $ kubectl apply -f known-hosts-configmap.yaml
    $ kubectl apply -f backup-config-configmap.yaml
    $ kubectl apply -f backup_compress_upload_s3.yaml
    $ kubectl apply -f pvc.yaml
    $ kubectl apply -f github_cron_aws.yaml
  
Edit below files and change values as per environment 
    
    1. "S3_upload" and change "S3_BUCKET" as per environment
    2. "back-config-example"
    3. "known-hosts-configmap.yaml"
    4. "private-key-secret.yaml"
   
