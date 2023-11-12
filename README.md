# Lab 6: Reproducibility
CI Server
  
## Asset Composition
- A Vagrant VM specification (i.e., Vagrant file)
- Ansible playbooks to provision the VM
- GitLab as VCS and CI running into the VM
- Docker service running into the VM

## Prerequisites
### Hardware
- Laptop with at least 8 GB memory (recommended: 16 GB, ideally 32 GB)

### Software
1. OS: Ubuntu 18.04
2. VirtualBox (v 6.0 or higher)
3. Vagrant (v 2.2.5 or higher)
4. Ansible (v 2.7.5 or higher)

## Guidelines
<br> <br>

1. **Get to the working directory:**
   ```bash
   cd ~/<git_root_folder>/devops/pipeline/s2-automate-build/integration-server
   ```

2. **Use Vagrant to create a VM, acting as the integration server:**

   ```bash
   vagrant up
   ```

3. **Edit `/etc/gitlab/gitlab.rb` and replace:**

   ```plaintext
   external_url http://hostname
   ```

   with:

   ```plaintext
   external_url 'http://192.168.56.9/gitlab'
   ```

   and replace:

   ```plaintext
   unicorn['port'] = 8080
   ```

   with:

   ```plaintext
   unicorn['port'] = 8088
   ```

   (Don't forget to uncomment)

4. **Reconfigure and restart GitLab:**

   ```bash
   sudo gitlab-ctl reconfigure
   sudo gitlab-ctl restart unicorn
   sudo gitlab-ctl restart
   ```
  ```
  Test Case 1:
  
  Initial conditions: None
  
  Test Steps:
  Go to http://192.168.56.9/gitlab
  
  Post conditions:
  - GitLab is accessible at the indicated URL
  - It asks to enter a password for the root credentials
  
  ```

5. **Set a password for the admin user:**
   
  Enter a password (referred to as `$YOUR_PASSWORD` later) for the root credentials.

  ```
  Test Case 2:
  Initial conditions: You have successfully entered a password for the root credentials
  Test Steps:
  
  1. Go to http://192.168.56.9/gitlab
  2. Log in using the username "root" and the password entered in the previous step.
  
  Post conditions:
  You have successfully logged in as an administrator
  ```

**Hint:** Feel free to use and modify this Markdown file for your GitHub repository's `README.md`.
