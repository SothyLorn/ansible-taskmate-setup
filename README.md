Prerequisite: 
- python3
- python3-pip: ``` apt install -y python3-pip ```
- ansible: ``` pip3 install ansible --break-system-packages```
- DigitalOcean API Token (full access)
- Check your python3 path (```which python3```) then put it in ./hosts (ansible_python_interpreter=/usr/bin/python3)
- ```ansible-galaxy collection install community.digitalocean```
- ```pip3 install dopy>=0.3.2 --break-system-packages```

Please clone/fork this project to your personal github/gitlab account first
```git clone https://github.com/SothyLorn/ansible-taskmate-setup.git```

I. Update environment variables or File 
1. DigitalOcean Token
File: ```ansible/roles/droplets/defaults/main.yml```
```bash
# defaults file for ansible/roles/droplets
do_token: ""
do_ssh_key: ""
```
=> do_token: Digital Ocean API Token

Steps to Generate DigitalOcean API Token (Full Access)

- Log in to DigitalOcean

  - Go to https://cloud.digitalocean.com/
  - Sign in with your DigitalOcean account credentials

- Navigate to API Settings
  * Method 1 (Direct):
    - Click on "API" in the left sidebar menu
  * Method 2 (Through Settings):
    - Click on your profile/avatar in the top right corner
    - Select "API" from the dropdown menu

- Generate New Token with Full Access
    In the API page
      - Look for the "Tokens/Keys" tab or "Personal Access Tokens" section
      - Click the "Generate New Token" button

    Configure Token Settings
      - Token Name: Enter a descriptive name (e.g., "Jenkins-Ansible-Full-Access" or "Automation-Full-Access")
      - Expiration: Choose expiration period:
      - 30 days (Recommended for security)
      - 60 days
      - 90 days
      - No expiry (not recommended)
      - Custom

- Set Permissions (IMPORTANT - Full Access):

    ✅ Check BOTH boxes

    ☑️ Read - Allows viewing resources
    ☑️ Write - Allows creating, modifying, and deleting resources


    - This gives full access to manage all DigitalOcean resources

- Generate Token
    - Click "Generate Token" button
- Copy and Save Your Token Immediately
    ⚠️ CRITICAL
      - The token will be displayed only once
      - Copy the entire token immediately
      - Store it in a secure location right away
      - Once you navigate away, you'll never see it again
      - If lost, you must delete this token and create a new one
      - Full Access Token Example Format:
          ```dop_v1_1234567890abcdef1234567890abcdef1234567890abcdef1234567890ab```

=> do_ssh_key: Digital Ocean SSH Key Name on your digitalocean account

Steps to View SSH Key Names in DigitalOcean1. Log in to DigitalOcean
  - Go to https://cloud.digitalocean.com/
  - Sign in with your DigitalOcean account credentials
  * Navigate to SSH Keys Settings
    * Method 1 (Direct)
      - Click on "Settings" in the left sidebar menu
      - Click on "Security" tab
      - Scroll down to the "SSH keys" section
    * Method 2 (Quick Access)
      - Click on your profile/avatar in the top right corner
      - Select "Settings" from the dropdown
      - Navigate to "Security" tab
      - Find "SSH keys" section
     * View Your SSH KeysIn the SSH keys section, you'll see a list of all your SSH keys with:
      - Name - The name you gave to the SSH key (e.g., "My Laptop", "Jenkins Server", "Personal MacBook")
      - Fingerprint - Unique identifier for the key
      - Added - When the key was added

2. CloudFlare Account Email & Token
File: ```ansible/roles/cloudflare/defaults/main.yml```
```bash
---
# defaults file for ansible/roles/cloudflare
cloudflare_email: "your_cloud_flare_acccount_email"
cloudflare_api_token: ""
```
Steps to Get Cloudflare Global API Key1. Log in to Cloudflare
  => Go to https://dash.cloudflare.com/
  => Sign in with your Cloudflare account credentials
  * Navigate to API Tokens Page
    * Method 1 (Direct)
      - Click on your profile icon in the top right corner
      - Select "My Profile"
      - Click on "API Tokens" in the left sidebar
    * Method 2 (Quick Link)
      - Go directly to: https://dash.cloudflare.com/profile/api-tokens
  * Locate Global API KeyOn the API Tokens page, you'll see two sections:
      - API Tokens (newer, more secure method)
      - API Keys (legacy method)
      - Scroll down to the "API Keys" section and find:
      - Global API Key
      - Origin CA Key
  * View Your Global API Key
      - Find "Global API Key" row
      - It will show as "Global API Key" with a "View" button
      - Click "View" button
      - A popup will appear asking for your password
      - Enter Your Password
      - Type your Cloudflare account password
      - Click "View" or "Submit"
      - Copy the API Key
      - Your Global API Key will be displayed
      - Click the "Copy" button or manually select and copy the key
      - The key is a long string of letters and numbers
      - Example format:
          ```a1b2c3d4e5f6g7h8i9j0k1l2m3n4o5p6q7r8```
    
3. SSH Key for devops user
File: ```ansible/roles/users/files/authorized_keys/devops.keys```
=> Please copy your laptop public ssh key & jenkins public ssh key paste to this file
II. Run ansible playbook
```bash
ansible-playbook ansible/setup-server.yml -i ansible/hosts
```
```bash
ansible-playbook ansible/setup-taskmate.yml -i ansible/custom_hosts -e website=demo-ansible.sothy.site
```
