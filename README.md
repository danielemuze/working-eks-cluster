# working-eks-cluster using Terraform

To spinup a working EKS CLuster, do the following:
1. copy all .tf files into  directory
2. create your AWS IAM Role with programmatic access and save Secret Key ID and Access Key
3. run "aws configure" on your Terraform machine and input all the neccessary details
4. run terraform init, plan and apply


5. aws eks --region us-east-1 update-kubeconfig --name eks --profile terraform  (this command will create a context)

6. you might be required to install kubectl on your machine before you can access the k8s cluster (sudo snap install kubectl --classic)

#Note that you can only access the CLuster using the account that was used to create it hence the need to create new users and roles by creating a ClusterRole and ClusterRoleBinding then you create the equivalent JSON on IAM GUI on AWS.
