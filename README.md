# SSH Security
 Securing network devices with SSH
# SSH Connection Project: Switch and Router Configuration

## Overview
This project demonstrates how to configure SSH connections for secure remote access to a network switch and router. The setup includes configuring SSH for both devices, setting up privileged access, and ensuring the proper configuration for VTY (Virtual Terminal) and console access.

## Devices Involved
- **Switch**
- **Router**

## Part 1: Configure SSH on the Router

1. **Set Hostname & Domain**  
   ```bash
   R1(config)# hostname R1  
   R1(config)# ip domain-name amir.com
   ```

2. **Generate RSA Keys**  
   ```bash
   R1(config)# crypto key generate rsa modulus 1024
   ```

3. **Configure Username and Password**  
   ```bash
   R1(config)# username admin privilege 15 secret adminpass
   ```

4. **Enable SSH on VTY Lines**  
   ```bash
   R1(config)# line vty 0 4  
   R1(config-line)# transport input ssh  
   R1(config-line)# login local
   ```

5. **Set SSH Timeout and Retries**  
   ```bash
   R1(config)# ip ssh time-out 75  
   R1(config)# ip ssh authentication-retries 2
   ```

6. **Test SSH Connection from PC-A (Tera Term)**  
   - SSH to R1 using username `admin` and password `adminpass`.

## Part 2: Configure SSH on the Switch

1. **Set Hostname & Domain on Switch**  
   ```bash
   S1(config)# ip domain-name amir.com
   ```

2. **Generate RSA Keys**  
   ```bash
   S1(config)# crypto key generate rsa modulus 1024
   ```

3. **Configure Username and Password**  
   ```bash
   S1(config)# username admin privilege 15 secret adminpass
   ```

4. **Enable SSH on VTY Lines**  
   ```bash
   S1(config)# line vty 0 15  
   S1(config-line)# transport input ssh  
   S1(config-line)# login local
   ```

5. **Set SSH Timeout and Retries**  
   ```bash
   S1(config)# ip ssh time-out 75  
   S1(config)# ip ssh authentication-retries 2
   ```

## Part 3: Configure Basic Security on the Router

1. **Encrypt Passwords**  
   ```bash
   R1(config)# service password-encryption
   ```

2. **Create Strong Passwords**  
   ```bash
   R1(config)# enable secret Enablep@55  
   R1(config)# security passwords min-length 10
   ```

3. **Disable Telnet and Allow SSH Only**  
   ```bash
   R1(config)# line vty 0 4  
   R1(config-line)# transport input ssh
   ```

4. **Set Idle Timeout**  
   ```bash
   R1(config)# line console 0  
   R1(config-line)# exec-timeout 5 0
   ```

5. **Prevent Brute Force Attempts**  
   ```bash
   R1(config)# login block-for 30 attempts 2 within 120
   ```

## Part 4: SSH From the CLI on the Switch

1. **SSH to Router from Switch CLI**  
   ```bash
   S1# ssh -l admin 192.168.1.1
   ```
   - Log in with `admin` and `adminpass`.

## Part 5: Secure the Switch

1. **Encrypt Passwords**  
   ```bash
   S1(config)# service password-encryption
   ```

2. **Create Strong Passwords**  
   ```bash
   S1(config)# enable secret Enablep@55
   ```

3. **Disable Telnet and Allow SSH**  
   ```bash
   S1(config)# line vty 0 15  
   S1(config-line)# transport input ssh
   ```

4. **Set Idle Timeout**  
   ```bash
   S1(config)# line console 0  
   S1(config-line)# exec-timeout 10 0
   ```

5. **Prevent Brute Force Attempts**  
   ```bash
   S1(config)# login block-for 30 attempts 2 within 120
   ```

6. **Shutdown Unused Ports**  
   ```bash
   S1(config)# interface range f0/1-4 , f0/7-24 , g0/1-2  
   S1(config-if-range)# shutdown


