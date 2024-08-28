# Secure VPC Architecture with Public and Private Subnets for Production Environment
# Overview :
This project’s overview is depicted in the diagram below. The setup revolves around a Virtual Private Cloud (VPC) featuring both public and private subnets, thoughtfully distributed across two Availability Zones to ensure reliability.

Within each public subnet, there’s a NAT gateway to facilitate outbound internet connectivity and a load balancer node for effective traffic distribution.

On the other hand, the project’s servers reside in the private subnets. Their deployment and termination are automated through an Auto Scaling group, allowing them to dynamically adapt to workload changes. These servers play a pivotal role in receiving traffic from the load balancer and can access the internet through the NAT gateway when necessary

![image](https://github.com/user-attachments/assets/2c59841d-f160-4323-af8e-63d67fe59d5f)

# Step 1 :
# Create the VPC :
1.Open the Amazon VPC console by visiting https://console.aws.amazon.com/vpc/.

2.On the dashboard, click on “Create VPC.”

3.Under “Resources to create,” select “VPC and more.”

4.Configure the VPC

a. Provide a name for the VPC in the “Name tag auto-generation” field.

b. For the IPv4 CIDR block, leave it as default suggestion.

5.Configure the subnets:

a. Set the “Number of Availability Zones” to 2 for increased resiliency across multiple Availability Zones.

b. Specify the “Number of public subnets” as 2.

c. Specify the “Number of private subnets” as 2.

d. For NAT gateways, choose “1 per AZ” to enhance resiliency.

g. For VPC endpoints, you can choose “None” .

h. Regarding DNS options, clear the checkbox for “Enable DNS hostnames.”

Once you’ve configured all the settings, click “Create VPC.”

![image](https://github.com/user-attachments/assets/2e278e86-e5eb-4e90-bb8b-2fcb8991cedf)


![image](https://github.com/user-attachments/assets/efc72dea-e102-411c-bb41-4194dd66609f)



![image](https://github.com/user-attachments/assets/9decf139-db76-458b-82c2-96357ddeda2e)



![image](https://github.com/user-attachments/assets/0875725b-4739-4c90-8bb2-343642ef46cf)


6. Now you can see you have successfully Created VPC .


# Step 2:

# Creating the Auto Scaling Group :


![image](https://github.com/user-attachments/assets/a8a64e2d-76d5-4671-9739-f5b86fb384a1)


![image](https://github.com/user-attachments/assets/71c6a7ea-f67f-4ee7-b613-048aa9fc7d5c)


![image](https://github.com/user-attachments/assets/6fab54f8-355d-4078-ae17-b8c5ce9ccd5b)


![image](https://github.com/user-attachments/assets/6cbfa00b-dee8-4f37-af69-1c4fed65b214)


![image](https://github.com/user-attachments/assets/1383b1a0-7c97-45a1-b0b5-801a9343fead)


![image](https://github.com/user-attachments/assets/55c23a53-a05a-491e-ab10-1835427b0bde)


Now you have to choose the Key-pair you created.


![image](https://github.com/user-attachments/assets/763ba690-9d7a-4b6e-888a-ede9f9cb6eb8)


![image](https://github.com/user-attachments/assets/24f7966b-14c9-4370-831c-cde9fecf39e7)


![image](https://github.com/user-attachments/assets/2f993eee-6e75-49d6-99b7-d91458e82cc9)


![image](https://github.com/user-attachments/assets/476089e9-293a-4885-a5df-4b923ddd35d8)


2. Scroll Down and then Click “Next”.


![image](https://github.com/user-attachments/assets/af1f08f3-4b4a-4c36-9c15-3ac1e2e1dc63)


3. Scroll Down and then Click “Next”.


![image](https://github.com/user-attachments/assets/6c6bcb95-7a60-4fcb-84e3-a75e33b1581f)


4. Scroll Down and then Click “Next”.


![image](https://github.com/user-attachments/assets/ae1808a7-6bab-4980-ba4f-12d495e5c074)


5. Scroll Down and then Click “Skip to Review”.


![image](https://github.com/user-attachments/assets/75e9cd81-5874-4cab-ad31-240601e64749)


6. Now your are Successfully Created Auto Scaling Group.
7. Open the AWS Management Console.
8. Navigate to the EC2 console by clicking on “Services” in the top-left corner, then selecting “EC2” under the “Compute” section.
9. In the EC2 dashboard, you’ll find the “Instances” link on the left-hand navigation pane. Click on “Instances.”
10. Here, you should see the list of EC2 instances associated with your account. Look for the instances created by your Auto Scaling Group.
Since you mentioned that the Auto Scaling Group launched instances in different AZs, you can check the “Availability Zone” column to verify that these instances are indeed distributed across multiple AZs.

# Step 3 :

# Creating the Bastion Host :

1.Launch Instance as Specified below .


![image](https://github.com/user-attachments/assets/9d1af26b-f5fd-4028-a35c-9529ebc011da)


![image](https://github.com/user-attachments/assets/fc2c8b43-1404-4b33-b99d-253707b5d1e2)


![image](https://github.com/user-attachments/assets/ae343e9c-d2ce-4718-bc7e-b357cc503f04)


![image](https://github.com/user-attachments/assets/dfe3a0f6-c217-486d-b25d-52c91c4c52c3)


![image](https://github.com/user-attachments/assets/ee67de40-fc45-43b1-bceb-f2fb3c8ce741)


# Step 4:

# SSH into Private Instance

1.SSH into the Bastion Host Instance: To SSH into the private instances, we first need to connect to our Bastion host instance. From there, we’ll be able to SSH into the private instance.

2.Ensure the PEM File is Present on the Bastion Host: Additionally, make sure that the PEM file is present on the Bastion host. Without it, you won’t be able to SSH into the private instance from the Bastion host.

3.Open a Terminal: Open a terminal window on your local machine.

4.Execute the Following Commands:

a. If your PEM file is named something like <aws demo.pem>, you must remove spaces in the filename. Please rename the file to something like <aws_demo.pem>.

b. Copy the PEM file to the Bastion host using the scp command. Replace <pem file location> with the local and remote file paths, and <bastion host public IP> with the Bastion host's public IP address. 

Example:
scp -i /Users/mathesh/Downloads/aws_demo.pem /Users/mathesh/Downloads/aws_demo.pem ubuntu@34.229.240.123:/home/ubuntu

c. The above command will copy the PEM file from your computer to the Bastion host. Once the file is successfully copied, move on to the next step.

d. SSH into the Bastion host using the following command:

ssh -i aws_demo.pem ubuntu@34.229.240.123

e. After SSH into the Bastion host, use the ls command to check if the aws_demo.pem file is present. If it's not there, double-check your previous commands. 

f. Now, you can SSH into the private instance using the following command, replacing <private IP> with the private instance's IP address:

ssh -i aws_demo.pem ubuntu@<private IP>

g. We will deploy our application on one of the private instances to test the load balancer. h. After successfully SSHing into the private instance, create an HTML file using the Vim text editor:

vim demo.html

i. This will open the Vim editor. Copy and paste any HTML content you like into the editor. 

j. For example:

<!DOCTYPE html>
<html>
<head>
<title>Page Title</title>
</head>
<body>
<h1>This is an AWS Demo Production</h1>
</body>
</html>

k. After pasting the content, save the file by pressing ‘Esc’ to exit insert mode and then entering :wq to save. Finally, can start your Python HTTP server on port 8000 to deploy your application on the private instance:

python3 -m http.server 8000

Now, your application is deployed on the private instance on port 8000.

# Note :

We intentionally deployed the application on only one instance to check if the Load Balancer will distribute 50% of the traffic to one instance (which will receive a response) and 50% to another instance (which will not receive a response).

# Step 4 :

# Creating the Load Balancer : 

1.Access the EC2 Terminal.
2.Follow the steps outlined below.


![image](https://github.com/user-attachments/assets/01372caf-c4ec-4a1e-b006-910bfba3ba14)


![image](https://github.com/user-attachments/assets/a8e4de45-6b33-4f7e-b6e9-8b15a4a35949)


![image](https://github.com/user-attachments/assets/5d6c6e5b-4370-4958-a7a2-204fd6fdc4ed)


![image](https://github.com/user-attachments/assets/deeb5758-8402-45ed-944a-16f49ae929dc)


![image](https://github.com/user-attachments/assets/dd157c9a-285f-49ab-888d-de20fe2c3f8c)


![image](https://github.com/user-attachments/assets/f380f3a7-ad10-4c42-81bc-1ace9b81e289)


![image](https://github.com/user-attachments/assets/2e322720-2455-46a7-9bed-1ab4ba4d7e18)


![image](https://github.com/user-attachments/assets/13934ad4-fdd7-4b7b-83a5-db7aa4f433c9)


![image](https://github.com/user-attachments/assets/590d5dbc-460f-4cf5-874b-49472835846d)


![image](https://github.com/user-attachments/assets/34d1dcb7-01f4-4f82-9097-2e0f35b537ad)


![image](https://github.com/user-attachments/assets/ab77e062-31a6-426b-bc97-73a5621a7fd1)


![image](https://github.com/user-attachments/assets/51fb9f35-6b54-4bc8-b5d4-0d96820ca4b2)


![image](https://github.com/user-attachments/assets/83f9fc19-ed07-4e0c-99b4-a1c90cbb4f06)


![image](https://github.com/user-attachments/assets/3c4eb604-c0c5-45db-9083-d97b0c59cf5a)


![image](https://github.com/user-attachments/assets/5d03a982-29b8-44c5-a0ec-7c5941b5c511)


![image](https://github.com/user-attachments/assets/ecbd3d39-d560-470e-ad3b-c822170c89ad)




Now We Successfully deployed Application securely in Private instance , We can access it through Internet using Load Balancer Securely .


















































