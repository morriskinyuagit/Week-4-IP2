# A. vagrant file
    # The task generally is to automate configurations on a vagrant provisioned server using ansible playbooks.
    # Started by vagrant init to configure my vm. My vagrant file had the following; 
        1.Vagrant.configure("2") do |config|: 
        This line sets up the Vagrant configuration and specifies the  version of the configuration file. "2" refers to the configuration version and is the recommended version for most use cases.

        2. config.vm.box = "geerlingguy/ubuntu2004": 
        This line specifies the base box that will be used for creating the virtual machine. In this case, it's using the "geerlingguy/ubuntu2004" box, which is a pre-configured Ubuntu 20.04 image.

        3. config.vm.network "forwarded_port", guest: 3000, host: 3000:
        This line forwards port 3000 from the guest VM to port 3000 on the host machine. It allows you to access a service running on port 3000 in the VM from your host machine using the same port.

        4. config.vm.network "forwarded_port", guest: 5000, host: 5000: 
        Similar to the previous line, this one forwards port 5000 from the guest VM to port 5000 on the host machine.

        5. config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "38.54.63.89": 
        This line forwards port 80 from the guest VM to port 8080 on the host machine, but it also specifies the host_ip as "38.54.63.89." This means that only connections from the host machine with the IP address "38.54.63.89" will be allowed to access the VM on port 8080.

        6. config.vm.synced_folder ".", "/vagrant", disabled: true: 
        This line configures a synced folder that syncs files between the host and the guest VM. However, it is disabled (disabled: true), so no syncing will occur. The source directory on the host is ".", and the target directory in the VM is "/vagrant."

        7. config.vm.provider "virtualbox" do |vb|: 
        This block configures settings specific to the VirtualBox provider.

        8. vb.customize [ "modifyvm", :id, "--uartmode1", "disconnected" ]:
        This line customizes the VirtualBox virtual machine by modifying the UART (Universal Asynchronous Receiver/Transmitter) mode. It sets "uartmode1" to "disconnected," which can be useful for certain debugging or interaction scenarios.

        9. vb.memory = "2048": 
        This line sets the amount of memory (RAM) allocated to the VM to 2048 MB (2 GB).

        10. config.vm.provision "ansible" do |ansible|: 
        This block specifies that Ansible will be used for provisioning the VM. It includes the playbook file ("/Week-4-IP2/playbook.yml") that Ansible will use to configure the VM and sets the verbosity level to "v."
 # In summary, this Vagrantfile configures a virtual machine based on the "geerlingguy/ubuntu2004" box, forwards several ports from the VM to the host, customizes the VirtualBox settings, and specifies Ansible for provisioning with a playbook file. The synced folder feature is disabled, and there's a specific IP restriction for port 8080.

# B. playbook
    I setup a playbook intended to set up an Ubuntu Server 22.04 environment, and it uses Ansible to perform various tasks, including privilege escalation and applying specific roles to configure the system. The roles mentioned likely contain the actual tasks and configurations needed to set up the desired environment, and their details would be defined in separate role files.
 # Key components of my playbook
     1. name: 
     Setup wk6 on Ubuntu Server 22.04: This is a human-readable name or description for the playbook. It indicates that the playbook's purpose is to set up a specific environment.

    2. hosts: all:
     This specifies the target hosts where the playbook will be executed. In this case, it's set to "all," which means it will run on all hosts defined in your inventory.

    3. become: true:
     This means that Ansible will use privilege escalation to become the superuser (root) to execute tasks that require elevated permissions.

    4. remote_user: root: 
    This sets the remote user to "root," indicating that Ansible will connect to the target hosts using the root user.

    5. gather_facts: true: 
    This instructs Ansible to gather system facts from the target hosts, which provides information about the hosts' configuration, hardware, and software.

    6. become_method: sudo: 
    This specifies that the "sudo" command will be used for privilege escalation when becoming the superuser.

    6. become_user: root: 
    This sets the user to become when escalating privileges to "root."

    7. become_flags: -H -S -n: 
    These are additional flags passed to the "sudo" command when escalating privileges. The flags include "-H" (sets the home directory to the target user's home directory), "-S" (prompts for a password), and "-n" (avoids creating a new login session).

    8. vars: 
    This section allows you to define variables that can be used in your playbook. In this case, it sets the ansible_python_interpreter variable to specify the path to the Python 3 interpreter.

    9. roles: 
    This section lists the roles that will be applied during the playbook execution. Roles are a way to organize and reuse Ansible tasks and configurations. The playbook includes three roles: "vm-config," "docker-install," and "resolvecloned_wkdir."

# C. Roles
   As seen in my playbook, I created 3 roles namely
    - vm-config
    - docker-install
    - resolvecloned_wkdir.
 # vm-config
  This role is part of a larger playbook and is responsible for setting up a base system configuration, updating package information, and installing several essential packages and dependencies. These tasks ensure that the system is prepared for subsequent roles or tasks that may require these dependencies.
 # docker-install
  This role automates the installation and setup of Docker on an Ubuntu system, including the addition of the Docker GPG key, adding the Docker repository, installing Docker and related packages, creating a user for Docker, and installing necessary Python modules for Docker management. It also ensures that the Docker service is restarted after installation.
 # resolvecloned_wkdir.
 This role has three main tasks: cloning a Git repository into a specified directory, changing the working directory to that directory, and then running Docker Compose within that directory. This sequence of tasks is commonly used to set up and deploy applications or services stored in a Git repository within a specific working directory, and then manage them with Docker Compose.

 # D. Launching the app
 To launch the app, I used commands such as
  1. vagrant up
  2. vagrant ssh

# E. Git workflows
  This I used the following in summary
  1. git add .
  2. git commit -m ""
  3. git push origin master

