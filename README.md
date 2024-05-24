# Active Directory Setup on Windows Server 2012

This repository contains the steps and configurations for setting up Active Directory on a Windows Server 2012 virtual machine, along with setting up DHCP and NAT/RAS services. Each step includes a detailed description and accompanying images to help guide you through the process.

## Prerequisites

- VMware Workstation or another virtualization platform
- Windows Server 2012 ISO
- Windows 10 ISO (for client setup)

## Steps

### 1. Configure Network Adapters in VMware

Two NICs were configured for the Windows Server VM:
- **NIC 1:** NAT (for internet access)
- **NIC 2:** Local Private Network (for internal communication)

![1](https://github.com/iamabdullahifti/active_directory/assets/129957445/e98f1542-7b9b-45ef-908d-966ac7e5f9fd)

### 2. Rename Network Adapters

For ease of identification, the network adapters were renamed:
- **NIC 1:** Internet
- **NIC 2:** Internal Network
  
![2](https://github.com/iamabdullahifti/active_directory/assets/129957445/2df8612a-ebb5-44f9-9c78-b9e4332bed69)

### 3. Configure IP Address for Internal Network

The NIC on the Local Private Network was configured with:
- **IP Address:** 172.16.0.1
- **DNS Address:** 127.0.0.1 (loopback)

![3](https://github.com/iamabdullahifti/active_directory/assets/129957445/fe091582-cf88-4e58-b52d-c3c7ffdba904)


### 4. Open Server Manager

Opened Server Manager on Windows Server 2012.

![4](https://github.com/iamabdullahifti/active_directory/assets/129957445/66948a0c-8878-41cf-b9e5-b93d4c936f5f)


### 5. Add Roles and Features

Selected the Windows Server 2012 in the Add Roles and Features wizard.

![5](https://github.com/iamabdullahifti/active_directory/assets/129957445/77edef2d-d694-48e2-9c17-c7050d4f9fa8)


### 6. Install Active Directory Domain Services

Installed Active Directory Domain Services (AD DS).

![6](https://github.com/iamabdullahifti/active_directory/assets/129957445/7151fc5e-32d4-4f0c-97b9-b30b61add08d)


### 7. Configure Domain

Configured the domain as **domain.com**. The Windows Server restarted after this step.

![7](https://github.com/iamabdullahifti/active_directory/assets/129957445/5b34d062-1f94-4117-a978-18c29b190fdb)


### 8. Create Admin Folder in Active Directory

Created a new folder named **ADMINS** in Active Directory to organize admin accounts.

![8](https://github.com/iamabdullahifti/active_directory/assets/129957445/8c628384-3c51-4415-b9e6-691339365da9)


### 9. Create a New Admin User

Created a new user with the email **a-abdullah@domain.com**.

![9](https://github.com/iamabdullahifti/active_directory/assets/129957445/1e7458f5-e8ba-42ac-b25c-2a0e9fafee5a)


### 10. Assign Admin Access

Granted admin access to the user by adding it to the **Domain Admins** group.

![10](https://github.com/iamabdullahifti/active_directory/assets/129957445/23ca1389-2705-4a8d-81d3-8f9dca0c6e1f)


### 11. Install NAT/RAS

Installed NAT/RAS from the Add Roles and Features wizard.

![11](https://github.com/iamabdullahifti/active_directory/assets/129957445/1362a992-2886-4bf4-9b30-0bfb954ba6a8)


### 12. Configure NAT

Configured NAT using the Routing and Remote Access Wizard, selecting the Internet interface.

![12](https://github.com/iamabdullahifti/active_directory/assets/129957445/9a5148d7-0a00-4bf0-8809-c2fad0dca7dd)


### 13. Install DHCP

Installed DHCP from the Add Roles and Features wizard.

![13](https://github.com/iamabdullahifti/active_directory/assets/129957445/c70ec050-78c8-4f91-bf5e-5142ec6a7599)


### 14. Define New Scope in DHCP

Defined a new IPv4 scope in DHCP with:
- **IP Address Range:** 172.16.0.100 - 172.16.0.200
- **Default Gateway:** 172.16.0.1

![14](https://github.com/iamabdullahifti/active_directory/assets/129957445/4c218907-5836-4e78-8097-ea666eb70cfa)


### 15. Authorize DHCP Server

Authorized the DHCP server within the domain.

![15](https://github.com/iamabdullahifti/active_directory/assets/129957445/13c70eba-8f96-4b2b-ba6c-a1c194a33cef)


### 16. Create Domain Users with PowerShell

Created users in the domain using a PowerShell script.

![16](https://github.com/iamabdullahifti/active_directory/assets/129957445/7a01ae4a-f546-4f7c-9c98-8ca5971c40f0)


### 17. Finalize Windows Server Setup

Completed the setup of the Windows Server.

![17](https://github.com/iamabdullahifti/active_directory/assets/129957445/bb80b3f2-d124-482a-9395-d51e8f29428f)


### 18. Install Windows 10 on Client VM

Installed Windows 10 on a client VM within the private network.

![18](https://github.com/iamabdullahifti/active_directory/assets/129957445/3f1aaa2f-6ac6-44b8-b168-d320e64eb748)


### 19. Join Client to Domain

Joined the Windows 10 client to the **domain.com** domain from System Properties.

![19](https://github.com/iamabdullahifti/active_directory/assets/129957445/af4fdce5-8ae3-4b38-bce9-ac5381406a56)


### 20. Verify DHCP Assignment

Verified that the client received an IP address from the DHCP server.

![20](https://github.com/iamabdullahifti/active_directory/assets/129957445/88278f11-acb4-43af-83dd-f7c76986531a)


### 21. First Login as Admin

Signed into the Windows 10 client using the **a-abdullah@domain.com** admin account. Verified login using the `whoami` command, which showed **domain\\a-abdullah**.

![21](https://github.com/iamabdullahifti/active_directory/assets/129957445/00d510e7-ed72-4529-9668-15d98c1c9705)


### 22. Login as a Regular User

Logged in again using a regular user account **aabrev@domain.com**. Verified the login with `whoami` and `ipconfig` commands, which confirmed the domain and IP configuration.

![22](https://github.com/iamabdullahifti/active_directory/assets/129957445/fcd01591-ce0b-42a9-9ea7-ed0f4db70ce1)

### 23. Login as Another User

Logged in again using another user account **aabrev@domain.com**. Verified the login with the `whoami` command, which showed **domain\\aabrev**. Also checked the IP configuration with the `ipconfig` command, confirming the default gateway and IP address assigned by DHCP.

![23](https://github.com/iamabdullahifti/active_directory/assets/129957445/97f7ce07-46f1-4813-b61c-3bd24470cc6c)


### 24. Verify User Account Configuration

Verified the user account configuration for **aabrev@domain.com**. The `whoami` command showed **domain\\aabrev**. The `ipconfig` command showed the IP address and default gateway assigned by the DHCP server.

![24](https://github.com/iamabdullahifti/active_directory/assets/129957445/4c730e35-d3bf-43a2-a185-28aa30380330)



## Conclusion

This documentation outlines the step-by-step process for setting up Active Directory, DHCP, and NAT/RAS on a Windows Server 2012 virtual machine, and joining a Windows 10 client to the domain. Each step includes images to assist with the configuration process.

Feel free to contribute or suggest improvements to this setup guide.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

*Note: Make sure to replace the placeholder image paths (e.g., `images/network_adapters.png`) with the actual paths to your images.*
