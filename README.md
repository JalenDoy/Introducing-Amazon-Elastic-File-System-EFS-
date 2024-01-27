# Introducing-Amazon-Elastic-File-System-EFS-

<h2>Task 1: Creating a security group to access youtr EFS file system </h2>

1. In the AWS Management Console, on the Services menu, choose EC2.
2. In the navigation pane on the left, choose Security Groups.
3, Copy the Security group ID of the EFSClient security group to your text editor.
4. Choose Create Security Group and then enter the following settings:
     - Security Group Name: EFS Mount Target
     - Description: Inbound NFS access from EFS clients
     - VPC: Lab VPC
5. Under inbound rules, choose add rule and then configure:
     - Type: NFS
     - Source -> Custom and then enter the security group ID.
6. Choose Create security group

<p align="center">
<br/>
<img src="https://i.imgur.com/EEPOZ4N.png"/>

<h2>Task 2: Creating an EFS file system </h2>

1. On the services menu, choose EFS
2. Choose Create File System
3. Choose customize
4. On Step 1
     - Uncheck Enable automatic backups
     - Lifecycle Management: None
     - Tags:
         - Key: Name
         - Value: My First EFS File System
5. Choose Next
6. VPC: Lab VPC
7. Detach the default security group from each Availability Zone mount target by choosing the  check box on each default security group.
8. Attach the EFS Mount Target security group to each Availability Zone mount target by:
    - Selecting each Security groups check box.
    - Choosing EFS Mount Target.
9. Choose Next
10. On Step 3, Choose next
11. On Step 4: Choose Create 

<p align="center">
<br/>
<img src="https://i.imgur.com/EEPOZ4N.png"/>
