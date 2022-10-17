# Cloudformation template to create VPCs

Original source [https://www.yobyot.com/aws/aws-cloudformation-example-with-jump-server/2017/05/02/](https://www.yobyot.com/aws/aws-cloudformation-example-with-jump-server/2017/05/02/)

To deploy a new stack use the AWS CLI command:

``` cli
aws cloudformation create-stack --stack-name temp-stack-dev --template-body vpc-template.yaml --parameters Parameters/dev-parameters.json
```

To update an existing VPC use the AWS CLI command:

``` cli
aws cloudformation update-stack --stack-name temp-stack-dev --template-body vpc-template.yaml --parameters Parameters/dev-parameters.json
```

''' cli
eksctl create cluster \\n--name dev-cluster15 \\n--region us-east-2 \\n--with-oidc \\n--ssh-access \\n--ssh-public-key eks-us-east2
'''

''' cli
aws cloudformation update-stack --stack-name dev-test-vpc --template-body file://vpc-template.yaml --parameters file://Parameters/dev-test-parameters.json --capabilities CAPABILITY_IAM
'''

the reference file 'cidr-spreadsheet.xlsx' is used to calculate the VPC subnets planned for the Creative Intelligence AWS account

 9880  ssh-add eks-us-east2.pem
 9881  ssh ec2-user@18.119.157.101

flowlog pricing

<https://aws.amazon.com/cloudwatch/pricing/>

Transit GW Notes
Attaching a VPC to a TGW enables routing only.
The VPCs need to have rout table entries added that indicate where to route traffic to other VPCs
ie
vpc destination      target
A   10.0.0.0/16      local
A   10.0.0.0/8       tgw-xxx

B   10.1.0.0/16      local
B   10.0.0.0/8       tgw-xxx

There must also be a security groups that allows the traffic to flow

AWS::EC2::TransitGateway
<https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-transitgateway.html#cfn-ec2-transitgateway-associationdefaultroutetableid>

AWS::EC2::TransitGatewayAttachment
<https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-transitgatewayattachment.html>

AWS::EC2::TransitGatewayRouteTable
<https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-ec2-transitgatewayroutetable.html>

AWS::EC2::TransitGatewayVpcAttachment

Sample transit GW template
<https://www.yobyot.com/aws/how-to-create-an-aws-transit-gateway/2019/08/22/>

Creating the Transit Gateway

``` cli
aws cloudformation update-stack --stack-name dev-transit-gateway --template-body file://transit-gateway.yaml
```
