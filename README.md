# SSH Security
 Securing network devices with SSH
# SSH Connection Project: Switch and Router Configuration

## Overview
This project demonstrates how to configure SSH connections for secure remote access to a network switch and router. The setup includes configuring SSH for both devices, setting up privilege access, and ensuring the proper configuration for VTY (Virtual Terminal) and console access.

## Devices Involved
- **Switch**
- **Router**

## Configuration Details

### Passwords:
- **Privilege Password:** `class`
- **VTY Line Password:** `cisco`
- **Console Line Password:** `cisco`

### Domain Name:
- **Domain:** `amir.net`

## Steps to Set Up SSH Connection

### 1. **Enable SSH on the Router**
   - Set the domain name:
     ```bash
     Router(config)# ip domain-name amir.net
     ```
   - Generate RSA keys:
     ```bash
     Router(config)# crypto key generate rsa
     ```
   - Set the SSH version:
     ```bash
     Router(config)# ip ssh version 2
     ```
   - Create a local user for SSH login:
     ```bash
     Router(config)# username admin privilege 15 secret <your_password>
     ```

### 2. **Configure Line VTY Access**
   - Configure VTY line access to accept SSH connections:
     ```bash
     Router(config)# line vty 0 4
     Router(config-line)# transport input ssh
     Router(config-line)# login local
     Router(config-line)# password cisco
     ```

### 3. **Configure Console Access**
   - Set the console line password:
     ```bash
     Router(config)# line con 0
     Router(config-line)# password cisco
     Router(config-line)# login
     ```

### 4. **Configure Privilege Mode Password**
   - Set the privilege password:
     ```bash
     Router(config)# enable secret class
     ```

### 5. **Save Configuration**
   - Save the configuration to ensure settings persist:
     ```bash
     Router# write memory
     ```

### 6. **Verify the SSH Configuration**
   - To test the SSH connection, use the following command from a remote machine:
     ```bash
     ssh admin@<router_ip_address>
     ```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
