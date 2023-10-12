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
  
![Screenshot 2023-10-11 at 12 16 39](https://github.com/SaintpatrickII/Azure-Database-Migration/assets/92804317/15c39cb4-7937-443f-91ae-fb808efe9101)
