# CloudFormation
01-StackConcept:
	Pre-requisties->
		default VPC,
		Keypar,
		AMI Id
02-Resource: Key components of stack 
	intrinsic Function !Ref
	Example :
	-------------
	AWSTemplateFormatVersion: 2010-09-09
	Description: Basic EC2 Instance.

	Resources:
		DevEC2Instance:
			Type: AWS::EC2::Instance
			Properties:
			ImageId: ami-0cd3dfa4e37921605
			InstanceType: t2.micro
			KeyName: cfn-key-1
			SecurityGroups:
				- default
				- !Ref SSHSecurityGroup # Assocation of security group  
		SSHSecurityGroup:
			Type: AWS::EC2::SecurityGroup
			Properties:
			GroupDescription: my new SSH SG
			SecurityGroupIngress:
				- IpProtocol: tcp
				  FromPort: '22'
				  ToPort: '22'
				  CidrIp: 0.0.0.0/0
				- IpProtocol: tcp
				  FromPort: '8080'
				  ToPort: '8080'
				  CidrIp: 0.0.0.0/0

		MyElasticIP:
			Type: AWS::EC2::EIP
			Properties:
				InstanceId: !Ref DevEC2Instance        # Assocation of Elsatic IP od EC2 instance   
	