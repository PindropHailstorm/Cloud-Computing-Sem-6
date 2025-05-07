VPC
![image](https://github.com/user-attachments/assets/3e3952dc-3855-4469-8ff1-84476ddc6228)
![image](https://github.com/user-attachments/assets/925324b5-ed52-4a0b-aa44-2774e6bdd5b7)

### Step 1: Create the VPC

1. Log in to the AWS Management Console.
2. Navigate to **VPC Dashboard**.
3. Click **Create VPC**:

### Step 2: Create Subnets

#### Zone A

1. Navigate to **Subnets** in the VPC Dashboard.
2. Click **Create Subnet**:
   - **Name**: `Public-Subnet-1`.
   - **VPC**: Select `My-VPC`.
   - **Availability Zone**: Select an AZ for Zone A (e.g., `us-east-1a`).
   - **CIDR Block**: `10.0.0.0/26`.
3. Click **Create Subnet**.
4. Repeat the process to create `Private-Subnet-1`:
   - **Availability Zone**: `us-east-1a`.
   - **CIDR Block**: `10.0.0.128/26`.

#### Zone B

1. Create `Public-Subnet-2`:
   - **Availability Zone**: Select an AZ for Zone B (e.g., `us-east-1b`).
   - **CIDR Block**: `10.0.0.64/26`.
2. Create `Private-Subnet-2`:
   - **Availability Zone**: `us-east-1b`.
   - **CIDR Block**: `10.0.0.192/26`.
### Step 3: Create an Internet Gateway (IGW)

1. Navigate to **Internet Gateways** in the VPC Dashboard.
2. Click **Create Internet Gateway**:
   - **Name**: `My-IGW`.
3. Click **Create**.
4. Attach the IGW to `My-VPC`:
   - Select the IGW → **Actions** → **Attach to VPC** → Choose `My-VPC`.
  
### Step 4: Create a Virtual Private Gateway (VPG)

1. Navigate to **Virtual Private Gateways** in the VPC Dashboard.
2. Click **Create Virtual Private Gateway**:
   - **Name**: `My-VPG`.
   - Leave the ASN as default.
3. Click **Create**.
4. Attach the VPG to `My-VPC`:
   - Select the VPG → **Actions** → **Attach to VPC** → Choose `My-VPC`.
### Step 5: Configure Route Tables

#### Public Route Table

1. Navigate to **Route Tables** in the VPC Dashboard.
2. Create a route table for public subnets:
   - Click **Create Route Table**.
   - **Name**: `Public-Route-Table`.
   - **VPC**: Select `My-VPC`.
3. Add a route for internet traffic:
   - Select the route table → **Routes** tab → **Edit Routes** → **Add Route**.
   - **Destination**: `0.0.0.0/0`.
   - **Target**: Select `My-IGW`.
4. Associate public subnets with the route table:
   - **Subnet Associations** → **Edit Subnet Associations** → Select `Public-Subnet-1` and `Public-Subnet-2`.
  
#### Private Route Table

1. Create a route table for private subnets:
   - Click **Create Route Table**.
   - **Name**: `Private-Route-Table`.
   - **VPC**: Select `My-VPC`.
2. Enable route propagation for the VPG:
   - Select the route table → **Route Propagation** tab → **Edit Route Propagation** → Select `My-VPG`.
3. Associate private subnets with the route table:
   - **Subnet Associations** → **Edit Subnet Associations** → Select `Private-Subnet-1` and `Private-Subnet-2`.

### Step 6: Launch EC2 Instances

#### Public Subnets

1. Launch an EC2 instance in `Public-Subnet-1`:
   - Select an AMI (e.g., Amazon Linux 2).
   - Configure networking to use `Public-Subnet-1`.
   - Assign a public IP address.
2. Repeat the process for `Public-Subnet-2`.

#### Private Subnets
1. Launch an EC2 instance in `Private-Subnet-1`:
   - **Step 1**: Navigate to the EC2 Dashboard and click **Launch Instance**.
   - **Step 2**: Choose an AMI (e.g., Amazon Linux 2 or Ubuntu).
   - **Step 3**: Choose an instance type (e.g., `t2.micro`).
   - **Step 4**: Configure instance details:
     - **Network**: Select `My-VPC`.
     - **Subnet**: Select `Private-Subnet-1`.
     - **Auto-assign Public IP**: Disable.
     - Leave other options as default or customize as needed.
   - **Step 5**: Add storage (default is fine).
   - **Step 6**: Add tags (optional, e.g., `Key: Name`, `Value: Private-Instance-1`).
   - **Step 7**: Configure security group:
     - Create or select a security group that allows SSH access from a specific IP or CIDR block.
   - **Step 8**: Review and launch:
     - Select an existing key pair or create a new one for SSH access.
     - Click **Launch**.

2. Repeat the process for `Private-Subnet-2`, selecting the corresponding subnet.
