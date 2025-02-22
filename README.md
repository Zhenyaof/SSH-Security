# SSH Security
 Securing network devices with SSH
# SSH Connection Project: Switch and Router Configuration

## Overview
This project demonstrates how to configure SSH connections for secure remote access to a network switch and router. The setup includes configuring SSH for both devices, setting up privilege access, and ensuring the proper configuration for VTY (Virtual Terminal) and console access.

## Devices Involved
- **Switch**
- **Router**

## Configuration Details

## Part 1: Configure SSH on the Router and Switch
1. **Set Hostname & Domain**  
   ```bash
   R1(config)# hostname R1  
   R1(config)# ip domain-name amir.com

R1(config)# crypto key generate rsa modulus 1024

R1(config)# username admin privilege 15 secret adminpass

R1(config)# line vty 0 4  
R1(config-line)# transport input ssh  
R1(config-line)# login local

R1(config)# ip ssh time-out 75  
R1(config)# ip ssh authentication-retries 2

The same applied to the Switch

## Part 2: Configure Basic Security on the Router
R1(config)# service password-encryption


