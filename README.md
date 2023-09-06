# working-eks-cluster using Terraform

To spinup a working EKS CLuster, do the following:
1. copy all .tf files into  directory
2. create your AWS IAM Role with programmatic access and save Secret Key ID and Access Key
3. run "aws configure --profile terraform" on your Terraform machine and input all the neccessary details
4. run terraform init, plan and apply


5. aws eks --region us-east-1 update-kubeconfig --name eks --profile terraform  (this command will create a context)

6. you might be required to install kubectl on your machine before you can access the k8s cluster (sudo snap install kubectl --classic)

#Note that you can only access the CLuster using the account that was used to create it hence the need to create new users and roles by creating a ClusterRole and ClusterRoleBinding then you create the equivalent JSON on IAM GUI on AWS.

7. Create an IAM group an attach policy to it.
8. Create a user and add to the group
9. Use the Secret Key and ID for user to generate an EKS profile as in nos. 3 above
10. Edit ConfigMap using the Admin credential (#kubectl edit -n kube-system configmap/aws-auth) then add then add the entry for the EKS Developer RBAC.

mapUsers: |
  - userarn: #arn for user created in IAM
    username: #username of choice
    groups:
    - #name of the group in the RBAC.yml file
Then save.

My own example of this file would be as below:

## Please edit the object below. Lines beginning with a '#' will be ignored,
## and an empty file will abort the edit. If an error occurs while saving this file will be
## reopened with the relevant failures.

apiVersion: v1
data:
  mapUsers: |
    - usernarn: arn:aws:iam::287259957274:user/eksdeveloper
      username: eksdeveloper
      groups:
      - reader
  mapRoles: |
  
  **************** OTHER CONFIG PART *************************

11. Create a kube config for the new user as in nos. 5 above
#aws eks --region us-east-1 update-kubeconfig --name eks --profile eksdeveloper

12. Check the profile being used to access the cluster using the command below:
#kubectl config view --minify

