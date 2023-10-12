# azure-Database-Migration

# Milestone 2 Set up the Production Environment:

1. Provision a Windows Virtual Machine

- Before creating a VM, we need to create a Resource group that will later contain all the infrastructure needed for this project

![Screenshot 2023-10-11 at 11 42 10](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/8cee047a-aab3-40d9-9967-3da11aa54679)

- VM is created, here we name & configure the image as Windows 10, size Standard_B2ms will provide all the resources needed
  
![Screenshot 2023-10-11 at 12 01 48](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/611e3285-371d-489d-9902-a11703b8fd8c)

- Resource is created using Admin authentication, if user makes a Linux shell this will be done VIA SSH, for inbound ports RDP for Windows image & SSH for Linux image

- With a Windows image we will need to accept the licencing also
  
![Screenshot 2023-10-11 at 12 01 57](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/f4cef0b0-dee7-4e2c-9801-19795f18916b)

- Review & create image, this will take a few minutes then we can view the VM in Azure

![Screenshot 2023-10-11 at 12 07 50](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/166a6540-6886-41c2-8dfc-e5cc5ff9a4ca)

2. Connect to the Windows Virtual Machine

- Click the 'Connect' icon at the top right of the resource
  
![Screenshot 2023-10-11 at 12 16 39](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/15c39cb4-7937-443f-91ae-fb808efe9101)

- This brings you to a page where we can download the RDP file to add the VM

![Screenshot 2023-10-11 at 12 18 06](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/c7708431-9217-4472-ae2b-a5350d4459dc)

![Screenshot 2023-10-11 at 12 18 23](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/e03dad7e-5c7d-425a-8cae-63d4328b788c)

- Find Windows Remote Desktop on the app store download this application, once open we can drag & drop the .rdp file to access the VM

<img width="693" alt="Screenshot 2023-10-11 at 12 21 54" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/67dfb943-5a1c-4b9f-9dc0-710f889821d6">

<img width="352" alt="Screenshot 2023-10-11 at 12 22 24" src="https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/7c0cf0e2-306a-4d9d-b3d3-afac9f3ea692">
