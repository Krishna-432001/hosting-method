# hosting-method
Here's a step-by-step guide to hosting a website using **GoDaddy** and **AWS**:

---

### **Option 1: Hosting with GoDaddy**
#### **1. Purchase Domain Name**
- Go to [GoDaddy's website](https://www.godaddy.com/).
- Search for your desired domain name.
- Add the domain to your cart and complete the purchase.

#### **2. Purchase Hosting (Optional if using GoDaddy Hosting)**
- If you want GoDaddy to host your website, purchase one of their hosting plans (e.g., shared hosting, WordPress hosting, or VPS hosting).
- Configure the hosting for your domain after purchase.

#### **3. Set Up Hosting**
- Access your GoDaddy account, go to **My Products** → **Web Hosting**.
- Click **Set Up** next to your hosting plan and choose your domain.
- Upload your website files using **cPanel** or **FTP**:
  - Use File Manager in cPanel to upload files to the `/public_html` folder.
  - Alternatively, configure FTP using credentials from cPanel.

#### **4. Configure DNS Settings (Optional)**
- If you are hosting elsewhere (e.g., AWS), you will need to configure DNS:
  - Go to **Domains** → Select your domain → **Manage DNS**.
  - Update the **A Record** or **Nameservers** with the details from your hosting provider.

---

### **Option 2: Hosting with AWS**
#### **1. Create an AWS Account**
- Go to [AWS](https://aws.amazon.com/) and sign up.
- Verify your identity using your phone number and payment method.

#### **2. Set Up an EC2 Instance**
1. **Launch an EC2 Instance**:
   - Open the **EC2 Dashboard** and click **Launch Instance**.
   - Choose an AMI (Amazon Machine Image) such as Ubuntu or Amazon Linux.
   - Select an instance type (e.g., t2.micro for free tier).
   - Configure instance details, such as default VPC and subnet.
   - Add storage and tags (if needed).
   - Configure security group:
     - Allow HTTP (port 80) and HTTPS (port 443) access.

2. **Launch the Instance**:
   - Review the settings and click **Launch**.
   - Create a new key pair or use an existing one to connect securely.

#### **3. Deploy Your Website**
1. **Access the Server**:
   - Use an SSH client (e.g., PuTTY or Terminal) to connect to the server:
     ```bash
     ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
     ```

2. **Install Web Server**:
   - For Ubuntu:
     ```bash
     sudo apt update
     sudo apt install apache2
     ```
   - For Amazon Linux:
     ```bash
     sudo yum update
     sudo yum install httpd
     sudo systemctl start httpd
     sudo systemctl enable httpd
     ```

3. **Upload Website Files**:
   - Use SCP (Secure Copy Protocol) to transfer files:
     ```bash
     scp -i "your-key.pem" /path/to/website-files ec2-user@your-ec2-public-ip:/var/www/html
     ```

#### **4. Configure DNS (Using GoDaddy Domain)**
1. **Get the Elastic IP**:
   - In the EC2 dashboard, allocate and associate an Elastic IP with your instance.

2. **Point Domain to AWS**:
   - Go to GoDaddy **Manage DNS**.
   - Update the **A Record** with the Elastic IP.

#### **5. Test Your Website**
- Open your browser and go to your domain. Your website should now be live.

---

### **Tips for Both Platforms**
- **SSL Certificate**:
  - GoDaddy: Install an SSL certificate via cPanel.
  - AWS: Use AWS Certificate Manager or Let's Encrypt.
  
- **Backups**:
  - Enable automatic backups for GoDaddy hosting.
  - Use AWS Snapshots to back up your EC2 instance.

Let me know if you need further clarification!
