# Ansible Role - MQ Install 

The "mq-automation" Ansible role is designed to automate the process of setting up and managing IBM MQ (Message Queue) infrastructure. It comprises a series of tasks that collectively handle the preparation of the operating system, creation of the MQ user and group, setup of necessary file systems, downloading and staging of the MQ software, installation of the software, creation of Queue Managers, creation of queues (based on a condition), and starting or stopping the Queue Managers. By leveraging this Ansible role, users can streamline the deployment and management of IBM MQ, ensuring consistent and efficient configuration while reducing manual effort and potential errors.

# Task Chart

```mermaid
%%{ init: { "flowchart": { "curve": "bumpX" } } }%%
flowchart LR
	%% Start of the playbook 'playbook.yaml'
	playbook_cb299955("playbook.yaml")
		%% Start of the play 'Play: all (6)'
		play_b5806164["Play: all (6)"]
		style play_b5806164 fill:#7e4e58,color:#ffffff
		playbook_cb299955 --> |"1"| play_b5806164
		linkStyle 0 stroke:#7e4e58,color:#7e4e58
			%% Start of the role 'mq-install'
			play_b5806164 --> |"1"| role_e5210075
			linkStyle 1 stroke:#7e4e58,color:#7e4e58
			role_e5210075("[role] mq-install")
			style role_e5210075 fill:#7e4e58,color:#ffffff,stroke:#7e4e58
				task_8b2e069a[" mq-install : kernel.shmmni"]
				style task_8b2e069a stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"1"| task_8b2e069a
				linkStyle 2 stroke:#7e4e58,color:#7e4e58
				task_b852fd0c[" mq-install : kernel.shmall"]
				style task_b852fd0c stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"2"| task_b852fd0c
				linkStyle 3 stroke:#7e4e58,color:#7e4e58
				task_7e7598d5[" mq-install : kernel.shmmax"]
				style task_7e7598d5 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"3"| task_7e7598d5
				linkStyle 4 stroke:#7e4e58,color:#7e4e58
				task_d4bf8937[" mq-install : kernel.sem"]
				style task_d4bf8937 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"4"| task_d4bf8937
				linkStyle 5 stroke:#7e4e58,color:#7e4e58
				task_80c3df9f[" mq-install : fs.file-max"]
				style task_80c3df9f stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"5"| task_80c3df9f
				linkStyle 6 stroke:#7e4e58,color:#7e4e58
				task_c2392d79[" mq-install : Hard nofile"]
				style task_c2392d79 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"6"| task_c2392d79
				linkStyle 7 stroke:#7e4e58,color:#7e4e58
				task_39683bb5[" mq-install : Soft nofile"]
				style task_39683bb5 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"7"| task_39683bb5
				linkStyle 8 stroke:#7e4e58,color:#7e4e58
				task_c48ab1f0[" mq-install : Install policy core utils"]
				style task_c48ab1f0 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"8"| task_c48ab1f0
				linkStyle 9 stroke:#7e4e58,color:#7e4e58
				task_75caf78d[" mq-install : Create the group for mqm user"]
				style task_75caf78d stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"9"| task_75caf78d
				linkStyle 10 stroke:#7e4e58,color:#7e4e58
				task_beff52a1[" mq-install : Create the user for mqm"]
				style task_beff52a1 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"10"| task_beff52a1
				linkStyle 11 stroke:#7e4e58,color:#7e4e58
				task_e7f3599d[" mq-install : Set up MQ user's env vars"]
				style task_e7f3599d stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"11"| task_e7f3599d
				linkStyle 12 stroke:#7e4e58,color:#7e4e58
				task_8ab6d2ba[" mq-install : Set up MQ user's sudoer privleges"]
				style task_8ab6d2ba stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"12"| task_8ab6d2ba
				linkStyle 13 stroke:#7e4e58,color:#7e4e58
				task_fd7be95c[" mq-install : Create MQStorageVG"]
				style task_fd7be95c stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"13 [when: 'MQStorageVG' not in ansible_facts.lvm.vgs.keys()|list]"| task_fd7be95c
				linkStyle 14 stroke:#7e4e58,color:#7e4e58
				task_ec2269ec[" mq-install : Create the LV for MQ Storage"]
				style task_ec2269ec stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"14 [when: 'MQStorageVG' not in ansible_facts.lvm.vgs.keys()|list]"| task_ec2269ec
				linkStyle 15 stroke:#7e4e58,color:#7e4e58
				task_1f08dcdb[" mq-install : set_fact"]
				style task_1f08dcdb stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"15"| task_1f08dcdb
				linkStyle 16 stroke:#7e4e58,color:#7e4e58
				task_77d21384[" mq-install : debug"]
				style task_77d21384 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"16"| task_77d21384
				linkStyle 17 stroke:#7e4e58,color:#7e4e58
				task_2cc7597e[" mq-install : Reset the fact for our primary partition in case we got NVME ssd"]
				style task_2cc7597e stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"17 [when: 'drbdpool' not in ansible_facts.lvm.vgs.keys()|list and 'nvme' in rdqm_storage_dev]"| task_2cc7597e
				linkStyle 18 stroke:#7e4e58,color:#7e4e58
				task_9fdbe793[" mq-install : Part up the Device"]
				style task_9fdbe793 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"18 [when: 'drbdpool' not in ansible_facts.lvm.vgs.keys()|list]"| task_9fdbe793
				linkStyle 19 stroke:#7e4e58,color:#7e4e58
				task_000cacbe[" mq-install : Configure the DRBD pool storage device"]
				style task_000cacbe stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"19 [when: 'drbdpool' not in ansible_facts.lvm.vgs.keys()|list]"| task_000cacbe
				linkStyle 20 stroke:#7e4e58,color:#7e4e58
				task_6d800217[" mq-install : Set fact for Linux as our OS"]
				style task_6d800217 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"20 [when: 'rhel' in os or 'centos' in os]"| task_6d800217
				linkStyle 21 stroke:#7e4e58,color:#7e4e58
				task_3f31796b[" mq-install : Set fact for Ubuntu as our OS"]
				style task_3f31796b stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"21 [when: 'ubuntu' in os]"| task_3f31796b
				linkStyle 22 stroke:#7e4e58,color:#7e4e58
				task_0b118aff[" mq-install : Download MQ Advanced for Developers"]
				style task_0b118aff stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"22"| task_0b118aff
				linkStyle 23 stroke:#7e4e58,color:#7e4e58
				task_3b753bd1[" mq-install : Extract MQ fom TAR"]
				style task_3b753bd1 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"23"| task_3b753bd1
				linkStyle 24 stroke:#7e4e58,color:#7e4e58
				task_9378f43b[" mq-install : Accept MQ License"]
				style task_9378f43b stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"24"| task_9378f43b
				linkStyle 25 stroke:#7e4e58,color:#7e4e58
				task_053f0714[" mq-install : Collect a list of MQ packages to install"]
				style task_053f0714 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"25"| task_053f0714
				linkStyle 26 stroke:#7e4e58,color:#7e4e58
				task_ea281768[" mq-install : debug"]
				style task_ea281768 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"26"| task_ea281768
				linkStyle 27 stroke:#7e4e58,color:#7e4e58
				task_5313ddee[" mq-install : Install MQ Software RPMS"]
				style task_5313ddee stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"27 [when: os == 'rhel']"| task_5313ddee
				linkStyle 28 stroke:#7e4e58,color:#7e4e58
				task_e3225d2b[" mq-install : Install MQ Software DEB files"]
				style task_e3225d2b stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"28 [when: os == 'ubuntu']"| task_e3225d2b
				linkStyle 29 stroke:#7e4e58,color:#7e4e58
				task_e31d0ade[" mq-install : Run setmqinst on primary nodes"]
				style task_e31d0ade stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"29 [when: 'primary' in mq_role]"| task_e31d0ade
				linkStyle 30 stroke:#7e4e58,color:#7e4e58
				task_7e55f38d[" mq-install : Get our DRBD kmod version and set it as a fact"]
				style task_7e55f38d stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"30 [when: enable_rdqm|bool]"| task_7e55f38d
				linkStyle 31 stroke:#7e4e58,color:#7e4e58
				task_99e3d2f2[" mq-install : Collect a list of pacemaker packages to install"]
				style task_99e3d2f2 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"31 [when: enable_rdqm|bool]"| task_99e3d2f2
				linkStyle 32 stroke:#7e4e58,color:#7e4e58
				task_b83dbe8a[" mq-install : Collect a list of drbd packages to install"]
				style task_b83dbe8a stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"32 [when: enable_rdqm|bool]"| task_b83dbe8a
				linkStyle 33 stroke:#7e4e58,color:#7e4e58
				task_cde13290[" mq-install : Grab the name of the RDQM package to install"]
				style task_cde13290 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"33 [when: enable_rdqm|bool]"| task_cde13290
				linkStyle 34 stroke:#7e4e58,color:#7e4e58
				task_8e885383[" mq-install : Install DRBD kmod"]
				style task_8e885383 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"34 [when: enable_rdqm|bool]"| task_8e885383
				linkStyle 35 stroke:#7e4e58,color:#7e4e58
				task_04be6063[" mq-install : Install pacemaker packages"]
				style task_04be6063 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"35 [when: enable_rdqm|bool]"| task_04be6063
				linkStyle 36 stroke:#7e4e58,color:#7e4e58
				task_df3b382e[" mq-install : Install drbd packages"]
				style task_df3b382e stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"36 [when: enable_rdqm|bool]"| task_df3b382e
				linkStyle 37 stroke:#7e4e58,color:#7e4e58
				task_66c79a6c[" mq-install : Install RDQM Package"]
				style task_66c79a6c stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"37 [when: enable_rdqm|bool]"| task_66c79a6c
				linkStyle 38 stroke:#7e4e58,color:#7e4e58
				task_decdbedb[" mq-install : Set the SELinux Context for drbd"]
				style task_decdbedb stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"38 [when: enable_rdqm|bool]"| task_decdbedb
				linkStyle 39 stroke:#7e4e58,color:#7e4e58
				task_b386f8ed[" mq-install : Set the mq user to be in the haclient group"]
				style task_b386f8ed stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"39 [when: enable_rdqm|bool]"| task_b386f8ed
				linkStyle 40 stroke:#7e4e58,color:#7e4e58
				task_d209406c[" mq-install : Generate the rdqm.ini file for primary hosts"]
				style task_d209406c stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"40 [when: enable_rdqm|bool and 'active' in dr_state]"| task_d209406c
				linkStyle 41 stroke:#7e4e58,color:#7e4e58
				task_965bcfd3[" mq-install : Generate the rdqm.ini file for standby hosts"]
				style task_965bcfd3 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"41 [when: enable_rdqm|bool and 'passive' in dr_state]"| task_965bcfd3
				linkStyle 42 stroke:#7e4e58,color:#7e4e58
				task_82683080[" mq-install : Enable the local cluster"]
				style task_82683080 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"42 [when: enable_rdqm|bool and createdrdqmprimary.changed]"| task_82683080
				linkStyle 43 stroke:#7e4e58,color:#7e4e58
				task_004a06a6[" mq-install : Enable the remote cluster"]
				style task_004a06a6 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"43 [when: enable_rdqm|bool and 'passive' in dr_state and createdrdqmstandby.changed]"| task_004a06a6
				linkStyle 44 stroke:#7e4e58,color:#7e4e58
				task_50efe308[" mq-install : Get a list of existing Queue Managers"]
				style task_50efe308 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"44"| task_50efe308
				linkStyle 45 stroke:#7e4e58,color:#7e4e58
				task_49363916[" mq-install : Set up the queue manager build template"]
				style task_49363916 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"45 [when: enable_rdqm|bool]"| task_49363916
				linkStyle 46 stroke:#7e4e58,color:#7e4e58
				task_91447211[" mq-install : Run the queue manager creation script on standby nodes"]
				style task_91447211 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"46 [when: enable_rdqm|bool and 'standby' in mq_role and qm.name not in qmgrlist.stdout_lines]"| task_91447211
				linkStyle 47 stroke:#7e4e58,color:#7e4e58
				task_212c57b5[" mq-install : Run the queue manager creation script on primary nodes"]
				style task_212c57b5 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"47 [when: enable_rdqm|bool and 'primary' in mq_role and qm.name not in qmgrlist.stdout_lines]"| task_212c57b5
				linkStyle 48 stroke:#7e4e58,color:#7e4e58
				task_101c5e51[" mq-install : Delete the created template files"]
				style task_101c5e51 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"48 [when: enable_rdqm|bool]"| task_101c5e51
				linkStyle 49 stroke:#7e4e58,color:#7e4e58
				task_95b8e5f4[" mq-install : Set up the queue manager MQSC file"]
				style task_95b8e5f4 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"49 [when: enable_rdqm|bool and 'primary' in mq_role and qm.is_ha|bool and not qm.is_dr|bool and qm.name not in qmgrlist.stdout_lines]"| task_95b8e5f4
				linkStyle 50 stroke:#7e4e58,color:#7e4e58
				task_0cec9d16[" mq-install : Apply the MQSC to the queue managers"]
				style task_0cec9d16 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"50 [when: enable_rdqm|bool and 'primary' in mq_role and qm.is_ha|bool and not qm.is_dr|bool and qm.name not in qmgrlist.stdout_lines and 'active' in dr_state]"| task_0cec9d16
				linkStyle 51 stroke:#7e4e58,color:#7e4e58
				task_cfe9aa8d[" mq-install : Clean up the template"]
				style task_cfe9aa8d stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"51 [when: enable_rdqm|bool and qm_create.changed]"| task_cfe9aa8d
				linkStyle 52 stroke:#7e4e58,color:#7e4e58
				task_4576e529[" mq-install : Get status of firewalld"]
				style task_4576e529 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"52 [when: enable_rdqm|bool]"| task_4576e529
				linkStyle 53 stroke:#7e4e58,color:#7e4e58
				task_d6f4f74f[" mq-install : Open firewall ports on all hosts"]
				style task_d6f4f74f stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"53 [when: enable_rdqm|bool and firewalld_service_status.status.ActiveState == 'active']"| task_d6f4f74f
				linkStyle 54 stroke:#7e4e58,color:#7e4e58
				task_bc2ccc0e[" mq-install : Generate our templated command files"]
				style task_bc2ccc0e stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"54 [when: create_queues|bool and 'primary' in mq_role and create_queues|bool]"| task_bc2ccc0e
				linkStyle 55 stroke:#7e4e58,color:#7e4e58
				task_077f8767[" mq-install : debug"]
				style task_077f8767 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"55 [when: create_queues|bool and 'primary' in mq_role and create_queues|bool]"| task_077f8767
				linkStyle 56 stroke:#7e4e58,color:#7e4e58
				task_f6e6b43d[" mq-install : Create the Queues"]
				style task_f6e6b43d stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"56 [when: create_queues|bool and 'primary' in mq_role and create_queues|bool and template_create.changed]"| task_f6e6b43d
				linkStyle 57 stroke:#7e4e58,color:#7e4e58
				task_e120d3c9[" mq-install : Dump the queue_create_out"]
				style task_e120d3c9 stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"57 [when: create_queues|bool and 'primary' in mq_role and create_queues|bool]"| task_e120d3c9
				linkStyle 58 stroke:#7e4e58,color:#7e4e58
				task_15324fdc[" mq-install : Clean up the template"]
				style task_15324fdc stroke:#7e4e58,fill:#ffffff
				role_e5210075 --> |"58 [when: create_queues|bool and 'primary' in mq_role and create_queues|bool]"| task_15324fdc
				linkStyle 59 stroke:#7e4e58,color:#7e4e58
			%% End of the role 'mq-install'
		%% End of the play 'Play: all (6)'
	%% End of the playbook 'playbook.yaml'

```
## Prepare the OS:

This task imports the tasks defined in the mq-os-setup.yaml file to prepare the operating system for IBM MQ installation.
It includes actions such as configuring OS settings and dependencies required for MQ.

- Configure Sysctl settings:

  - The code modifies various kernel parameters using the sysctl command to optimize system performance and resource allocation.
  - By adjusting parameters such as kernel.shmmni, kernel.shmall, kernel.shmmax, kernel.sem, and fs.file-max, we can fine-tune the behavior of the Linux kernel to better suit the needs of IBM MQ and potentially improve its performance. 


- Update PAM limits for the mqm group:

  - PAM (Pluggable Authentication Modules) limits define the maximum system resources available to users or groups.
  - In this case, the code updates the limits for the mqm group by setting the maximum number of open file descriptors (nofile) to 10240.
  - This ensures that IBM MQ processes, which run under the mqm group, have sufficient file descriptor limits to handle concurrent connections and messaging.


- Install policy core utils:

  - The code installs the policycoreutils-python-utils package using the DNF package manager.
  - This package provides essential utilities for managing SELinux (Security-Enhanced Linux) policies and permissions.
  - SELinux is a security framework that provides access controls and policy enforcement mechanisms to further secure the system. Installing the policy core utils is crucial for working with SELinux in an IBM MQ environment.

## Create the MQ User and Group:

This task imports the tasks defined in the mq-create-users.yaml file to create the necessary user and group entities for IBM MQ. It ensures that the dedicated MQ user and group are created with appropriate permissions and configurations.

- Create MQM User and Group:

  - This code block performs the necessary steps to create the mqm group and user.
  - The mqm group is created with a specified group ID (mqm_gid).
  - The mqm user is created with a specific user ID (mqm_uid) and assigned to the mqm group.
  - Creating a separate user and group for MQ helps maintain security and isolation for MQ processes.


- Set up MQ user's environment variables:

  - This task ensures that the MQ user (mqm) has the appropriate environment variables set up.
  - The .bashrc file, which contains environment configurations, is copied from the files/bashrc source to the MQ user's home directory (/home/mqm/.bashrc).
  - This file is owned by the mqm user and group, and it has read permissions (0644).
  - Setting up environment variables helps provide the necessary settings for the MQ user's session.


- Set up MQ user's sudoer privileges:

  - This task grants specific sudoer privileges to the MQ user (mqm).
  - The community.general.sudoers module is used to manage sudoers configurations.
  - It creates a sudoers file named mqm-user-privs and specifies that the mqm user should have the privileges to execute specific MQ-related commands (/opt/mqm/bin/crtmqm, /opt/mqm/bin/dltmqm, /opt/mqm/bin/rdqmadm, /opt/mqm/bin/rdqmstatus).
  - Additionally, the nopassword option is set to true, allowing the mqm user to execute these commands without a password prompt.

## Create the filesystems:

This task imports the tasks defined in the mq-filesystems.yaml file to create the required filesystems for MQ. It handles the setup and configuration of filesystems necessary for storing MQ data and log files.

- Configure MQ Storage Device:

  - This block of tasks executes only when the "MQStorageVG" volume group is not present on the system. It ensures that the necessary storage configuration is in place.
  - The community.general.lvg module is used to create the "MQStorageVG" volume group. It associates the volume group with the physical volume specified by the 'mq_storage_dev' variable.
  - Following that, the community.general.lvol module creates the "MQStorageLV" logical volume within the "MQStorageVG" volume group. The logical volume is sized to occupy 100% of the available free space within the volume group.


- Set Fact and Debug:

  - The set_fact task sets the part_name fact based on the value of the 'rdqm_storage_dev' variable. This fact determines the name of the storage device partition to be created.
  - The debug task is used to display the value of the 'part_name' fact for debugging purposes. It helps verify the correctness of the fact assignment.


- Create the DRBD Pool storage:

  - This block of tasks executes only when the "drbdpool" volume group is not present on the system, ensuring the required storage configuration for the DRBD (Distributed Replicated Block Device) pool.
  - If the 'rdqm_storage_dev' variable contains the substring "nvme," the part_name fact is modified by appending "p1" to the device name. This accounts for NVME SSD devices that use a different partition naming scheme.
  - The community.general.parted module creates a partition (number 1) on the rdqm_storage_dev device. The partition is formatted with the ext4 filesystem.
  - Finally, the community.general.lvg module is used to create the "drbdpool" volume group. It associates the volume group with the partition specified by the part_name fact.

## Download and stage MQ software:

This task imports the tasks defined in the mq-download.yaml file to download and stage the IBM MQ software. It handles the retrieval and preparation of the software package required for the subsequent installation steps. It dynamically creates a URL that allows for flexibility in fetching the appropriate software version, specific to either Linux or Ubuntu. This automation simplifies the setup and deployment of IBM MQ.

- Set fact for Linux as our OS:

  - This task sets the 'ouros' fact to "linux" when the target operating system is either RHEL (Red Hat Enterprise Linux) or CentOS.
  - By setting this fact, the code determines the appropriate download URL for the MQ software based on the Linux operating system.


- Set fact for Ubuntu as our OS:

  - This task sets the 'ouros' fact to "ubuntu" when the target operating system is Ubuntu.
  -  Similar to the previous task, this fact is used to determine the correct download URL for the MQ software specific to the Ubuntu operating system.


- Download MQ Advanced for Developers:

  - This task utilizes the get_url module to download the MQ Advanced for Developers software package.
  - The URL is constructed dynamically based on the 'mq_dl_url' variable, version variable (replacing periods with empty spaces), and the 'ouros' fact (representing the Linux distribution).
  -  The downloaded software is saved to the /tmp/mq.tar.gz file.
  -  This task is tagged with "download" for easy identification and selective execution.


- Extract MQ from TAR:

  - This task uses the unarchive module to extract the MQ software from the /tmp/mq.tar.gz archive.
  - The archive is extracted to the /tmp directory on the target system.
  - The remote_src option is set to "yes" to indicate that the source archive resides on the Ansible control machine.
  - Like the previous task, this task is tagged with "download."

## Install MQ software:

This task imports the tasks defined in the mq-install.yaml file to install the IBM MQ software on the target system.
It handles the installation process, including software verification and configuration.

- Accept MQ License:

  - This task runs the MQ license acceptance script by executing the mqlicense.sh -accept command in the /tmp/MQServer/ directory.
  - The output of the command is stored in the 'license_out' variable using the register keyword. This helps capture the result of the license acceptance process.


- Collect a list of MQ packages to install:

  - This task retrieves a list of MQ package files available in the /tmp/MQServer/ directory using the ls command.
  - The list of package files is stored in the 'packagelist' variable using the register keyword.


- Install MQ Software RPMS or DEB files:

  - Depending on the operating system (os), either RPM packages (for rhel) or DEB files (for ubuntu) are installed using the appropriate package manager (ansible.builtin.dnf or ansible.builtin.apt).
  - The package names to install are provided as the values of the 'packagelist.stdout_lines' variable.
  - The installation is performed with additional settings like disabling GPG check and ensuring the desired package state (present).


- Run setmqinst on primary nodes:

  - This task executes the `setmqinst` command, which initializes the MQ installation by setting the installation path (MQ_INSTALLATION_PATH).
  - The command is only executed on nodes where the "primary" role is assigned. This ensures that the MQ installation is properly configured on primary nodes only.


- Install RDQM block:
  - This RDQM block of tasks focuses on installing and configuring components related to RDQM, which enables the replication and disaster recovery capabilities of IBM MQ. It ensures data redundancy and high availability in messaging systems.
  
- Get the DRBD kmod version:

  - This task retrieves the version of the DRBD (Distributed Replicated Block Device) kernel module installed on the system.
  - The shell module executes the command `'/tmp/MQServer/Advanced/RDQM/PreReqs/{{ rel }}/kmod-drbd-9/modver'`, storing the output in the 'kmodver' variable using the register keyword.
  - The failed_when condition checks if the return code (rc) is 1, indicating a failure in retrieving the version. This allows for handling scenarios where the DRBD kernel module is not present.


- Collect a list of pacemaker packages to install:

  - This task retrieves a list of pacemaker packages available in the '/tmp/MQServer/Advanced/RDQM/PreReqs/{{ rel }}/pacemaker-2/' directory using the ls command.
  - The list of package files is stored in the 'pacemakerlist' variable using the register keyword.
  - The packages will be installed later to ensure the necessary dependencies for pacemaker are met.


- Collect a list of DRBD packages to install:

  - This task retrieves a list of DRBD packages available in the '/tmp/MQServer/Advanced/RDQM/PreReqs/{{ rel }}/drbd-utils-9/drbd-*/' directory using the ls command.
  - The list of package files is stored in the 'drbdlist' variable using the register keyword.
  - The packages will be installed later to ensure the necessary dependencies for DRBD are met.


- Grab the name of the RDQM package to install:

  - This task retrieves the name of the RDQM package available in the '/tmp/MQServer/Advanced/RDQM/MQSeriesRDQM-*' directory using the ls command.
  - The package name is stored in the 'rdqmpkg' variable using the register keyword.
  - This package will be installed later to enable RDQM features in IBM MQ.


- Install DRBD kmod:

  - This task uses the ansible.builtin.dnf module to install the DRBD kernel module (kmod-drbd) package.
  - The package path is constructed dynamically based on the retrieved version (kmodver.stdout), allowing for the installation of the specific version required by the system.
  - Additional settings such as disabling GPG check and ensuring the package state (present) are applied during installation.


- Install pacemaker packages:

  - This task uses the ansible.builtin.dnf module to install the pacemaker packages necessary for RDQM.
  - The package names are provided as values from the 'pacemakerlist.stdout_lines' variable.
  - Additional settings such as disabling GPG check and ensuring the package state (present) are applied during installation.


- Install DRBD packages:

  - This task uses the ansible.builtin.dnf module to install the DRBD packages required for RDQM.
  - The package names are provided as values from the 'drbdlist.stdout_lines' variable.
  - Additional settings such as disabling GPG check and ensuring the package state (present) are applied during installation.


- Install RDQM Package:

  - This task uses the ansible.builtin.dnf module to install the RDQM package.
  - The package name is provided as the value from the 'rdqmpkg.stdout' variable.
  - Additional settings such as disabling GPG check and ensuring the package state (present) are applied during installation.


- Set the SELinux Context for DRBD:

  - This task uses the shell module to execute the `semanage permissive -a drbd_t` command.
  - It sets the SELinux context to permissive for the DRBD component, allowing it to function properly within the SELinux security framework.


- Set the mq user to be in the haclient group:

  - This task uses the ansible.builtin.user module to add the "mqm" user to the "haclient" group.
  - The name parameter specifies the user to modify, and the groups parameter specifies the group to which the user should be added.
  - The append parameter ensures that the user is added to the group without removing any existing group memberships.


- Generate the rdqm.ini file for primary hosts:

  - This task generates the rdqm.ini configuration file for primary hosts using the ansible.builtin.template module.
  - The source template file (rdqm.ini.j2) and destination path (/var/mqm/rdqm.ini) are specified.
  - The owner, group, and mode parameters set the ownership and permissions of the generated file.
  - The 'hostgroup' variable is passed to the template, allowing customization based on the primary host's group.


- Generate the rdqm.ini file for standby hosts:

  - This task generates the rdqm.ini configuration file for standby hosts, similar to the previous task.
  - The generation occurs only if the host is in the "standby" group and the DR state includes "passive".
  - The 'hostgroup' variable is passed to the template, allowing customization based on the standby host's group.


- Enable the local cluster:

  - This task uses the shell module to execute the `/opt/mqm/bin/rdqmadm -c `command, enabling the local cluster for RDQM.
  - The register keyword captures the output and status of the command in the 'clusterconfigprimary' variable.
  - The task fails if the return code (rc) is not equal to 0, indicating a failure in enabling the local cluster.
  - The execution of this task depends on whether changes were made to the rdqm.ini file (createdrdqmprimary.changed).


- Enable the remote cluster:

  - This task uses the shell module to execute the `/opt/mqm/bin/rdqmadm -c` command, enabling the remote cluster for RDQM.
  - The register keyword captures the output and status of the command in the 'clusterconfigstandby' variable.
  - The task fails if the return code (rc) is not equal to 0, indicating a failure in enabling the remote cluster.
  - The execution of this task depends on whether changes were made to the rdqm.ini file for standby hosts (createdrdqmstandby.changed) and the DR state includes "passive".

## Create Queue Managers 

This task creates queue managers defined in the 'group_vars' (/solution-mq-rdqm-hadr/resources/ansible/mq-automation/group_vars/all/main.yml). The task is setup to handle HA (High Availability) and HADR (High Availability Disaster Recovery) configurations and setup of the queue managers on the nodes based on the desired configuration.

- Get a list of existing Queue Managers:

  - This task retrieves a list of currently existing queue managers using the `dspmq` command and some text processing with `awk` and `sed`.
  - The list of queue manager names is stored in the 'qmgrlist' variable using the register keyword.
  - This information helps determine if a queue manager needs to be created and which may already exist. 


- Create Queue Managers:

  - This block of tasks handles the creation of queue managers based on certain conditions.
  - The templates/create_qm.sh.j2 template file is used to generate a shell script for queue manager creation.
  - The shell script is created for each queue manager defined in the 'queuemgrs' list.
  - The generated script is then executed on both standby and primary nodes, depending on the mq_role and 'qmgrlist' conditions.
  - The generated script will look for  the desired state for each queue manager in the 'queuemgrs' list. Each queue manager has two variables called "is_dr" and "is_ha". These stand for "is disaster recovery" and "is high availability". Based on these desired states, specific MQ commands need to be run on the 'primary' and 'standby' host groups and 'primary' and 'standby' nodes. The script looks at the configuration of the inventory.ini file and uses this to setup the queue manager desired HA/HADR state on the nodes. 
  - After execution, the script files are deleted.
  - If the queue manager is marked as HA (High Availability) and not DR (Disaster Recovery), an additional MQSC (MQ Scripting Command) file template templates/qmgr_settings.mqsc.j2 is set up.
  - The MQSC file is applied to the queue managers, configuring specific settings related to channel, queues, security, and listener.
  - Once applied, the MQSC template file is cleaned up.


- Open the firewall if necessary:

  - This block of tasks manages the opening of firewall ports if the enable_rdqm variable is set to true.
  - It checks the status of the 'firewalld' service and, if active, opens the specified port for each queue manager defined in the 'queuemgrs' list.

## Create Queues 

This task imports the tasks defined in the mq-create-queues.yaml and is designed to automate the creation of queues within an IBM MQ environment. It consists of tasks that generate command files for queue creation and then execute those commands using the 'runmqsc' utility. The task is conditional, running only on primary nodes when the 'create_queues' variable is set to true. 

- Generate Command Files:

  - This block of tasks is executed on primary nodes when the 'create_queues' variable is set to true.
  - It generates command files for creating queues using a template file templates/create_queue.in.j2.
  - The template file is customized for each queue manager defined in the 'queuemgrs' list.
  - The resulting command files are stored in /tmp/ with the queue manager name as the filename.


- Create the Queues:

  - This task is executed when changes occur in the generated command files.
  - It runs the `runmqsc` command, which executes the command files to create queues within each queue manager.
  - The task is run as the mqm user using become_user.
  - The success or failure of the queue creation is determined based on the output of the `runmqsc` command.
  - If the queue creation fails, the task fails if the return code (rc) is not 0 or 10, and the output doesn't contain the message indicating no syntax errors.


- Clean Up:

  - After the queue creation task, the command files (*.in) generated earlier are removed to clean up the temporary files.

## Stop/Start MQ Queue Managers

This task imports the tasks defined in the mq-start-RDQM.yaml and mq-stop-RDQM.yaml and is designed to stop and start queue managers created during installation.


