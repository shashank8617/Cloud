# AWS VPC and Subnet Configuration

## VPC and Subnets

### Step 1: Create a VPC

1. Navigate to the VPC Dashboard in the AWS Management Console.
2. Click on "Create VPC".
3. Name your VPC (e.g., `MyFirstVPC`).
4. Set the IPv4 CIDR block to `10.0.0.0/16`.
5. Click "Create VPC".

### Step 2: Launch Two Instances in the VPC

1. Go to the EC2 Dashboard and click on "Launch Instance".
2. Choose an AMI and instance type.
3. In the "Configure Instance" step, select the VPC you created (`MyFirstVPC`).
4. Launch one instance in one Availability Zone (e.g., `us-east-1a`) and another in a different Availability Zone (e.g., `us-east-1b`).
5. Enable the option to assign a public IP address for both instances.
6. Configure security groups and key pairs as needed.
7. Launch the instances.

### Step 3: Create a New VPC with Subnets

1. Navigate to the VPC Dashboard.
2. Click on "Create VPC".
3. Name your VPC (e.g., `MySecondVPC`).
4. Set the IPv4 CIDR block to `172.16.0.0/16`.
5. Click "Create VPC".

### Step 4: Create Subnets within the New VPC

#### Public Subnet

1. In the VPC Dashboard, click on "Subnets".
2. Click "Create Subnet".
3. Name your subnet (e.g., `PublicSubnet`).
4. Select the `MySecondVPC` VPC.
5. Set the IPv4 CIDR block to `172.16.1.0/24`.
6. Choose an Availability Zone.
7. Click "Create Subnet".

#### Private Subnet

1. Click "Create Subnet".
2. Name your subnet (e.g., `PrivateSubnet`).
3. Select the `MySecondVPC` VPC.
4. Set the IPv4 CIDR block to `172.16.2.0/24`.
5. Choose a different Availability Zone if desired.
6. Click "Create Subnet".

## Route Tables

### Step 5: Create and Associate a New Route Table with a Public Subnet

1. Navigate to the VPC Dashboard and click on "Route Tables".
2. Click "Create route table".
3. Name your route table (e.g., `PublicRouteTable`).
4. Select the `MySecondVPC` VPC.
5. Click "Create route table".
6. Select the new route table and click on the "Subnet Associations" tab.
7. Click "Edit subnet associations".
8. Select the `PublicSubnet` and click "Save associations".

#### Verify Internet Access Loss

1. Edit the routes in the `PublicRouteTable`.
2. Remove the `0.0.0.0/0` route if it exists.
3. Launch an instance in the `PublicSubnet` and verify it has no internet access.

### Step 6: Edit the Route Table to Add an Internet Gateway

1. Navigate to the VPC Dashboard and click on "Internet Gateways".
2. Click "Create internet gateway".
3. Name the internet gateway (e.g., `MyIGW`).
4. Click "Create internet gateway".
5. Attach the internet gateway to the `MySecondVPC` VPC.
6. In the `PublicRouteTable`, click on the "Routes" tab and "Edit routes".
7. Add a route for `0.0.0.0/0` with the target set to the internet gateway (`MyIGW`).
8. Launch an instance in the `PublicSubnet` and verify it has internet access.

### Step 7: Create a Custom Route Table for a Private Subnet

1. Navigate to the VPC Dashboard and click on "Route Tables".
2. Click "Create route table".
3. Name your route table (e.g., `PrivateRouteTable`).
4. Select the `MySecondVPC` VPC.
5. Click "Create route table".
6. Select the new route table and click on the "Subnet Associations" tab.
7. Click "Edit subnet associations".
8. Select the `PrivateSubnet` and click "Save associations".

#### Add a Route for Internet Gateway and Observe Behavior

1. In the `PrivateRouteTable`, click on the "Routes" tab and "Edit routes".
2. Add a route for `0.0.0.0/0` with the target set to the internet gateway (`MyIGW`).
3. Launch an instance in the `PrivateSubnet` and verify it does not have internet access.

### Step 8: Modify the Route Table to Use a NAT Gateway

1. Navigate to the VPC Dashboard and click on "NAT Gateways".
2. Click "Create NAT gateway".
3. Select the `PublicSubnet` and allocate an Elastic IP.
4. Click "Create NAT gateway".
5. In the `PrivateRouteTable`, click on the "Routes" tab and "Edit routes".
6. Change the target for the `0.0.0.0/0` route to the NAT gateway.
7. Launch an instance in the `PrivateSubnet` and verify it has internet access.

By following these steps, you can set up a VPC with public and private subnets, configure route tables, and verify internet access for instances in different subnets.
