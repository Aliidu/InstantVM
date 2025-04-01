# InstantVM
Deploy Windows 10 &amp; Ubuntu 22.04 VMs with Vagrant, preconfigured for easy use

This project provides an easy way to deploy Windows 10 and Ubuntu Server 22.04 virtual machines using Vagrant and VirtualBox.

Each VM is automatically configured with essential settings for a fast deployment.

🌟 Features : 

    Dynamic creation of Windows 10 and/or Ubuntu 22.04 VMs

    Automatic keyboard configuration to AZERTY

    Enabled bidirectional drag-and-drop and clipboard sharing

    Optimized resource allocation (RAM, CPU)

    Communication via WinRM (Windows) and SSH (Ubuntu)

🛠️ Usage : 

    Install prerequisites:

        Vagrant

        VirtualBox

    Start the VMs:
    Run vagrant up and then specify your choice:

        All VMs: type all

        Windows 10: type windows

        Ubuntu: type ubuntu

    Access the VM:

        Windows: vagrant rdp win10-<timestamp>

        Ubuntu: vagrant ssh ubuntu-vm

💡 TO-DO List :  

    Add the option to choose between VMware Workstation and VirtualBox for virtualization.

📄 License : 

Open-source project, free to use and modify. ✨
