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
<img src="https://i.imgur.com/8moFBiw.png"/>

<h2>Task 3:  Connecting to your EC2 instance via SSH </h2>

1. In Vocarem, choose the details dropdown menu and then show
2. Choose Download PPK ans save the labsuser.ppk file
3. Note the EC2PublicIP address
4. Exit details panel
5. Open putty.exe, download if not installed
6. Choose connection -> Seconds between keepalives: 30
7. Choose Session
     - Host Name (or IP Address): Paste the EC2PublicIP
     - In putty, in the connection list, expand SSH
     - Choose Auth: Expand credentials and under Private Key File for authentication choose browse. Browse to the labsuser.ppk file and choose open
     - Open
8. Choose accept
9. Login as: ec2-user

<p align="center">
<br/>
<img src="https://i.imgur.com/i0J4iGc.png"/>

<h2>Task 4:  Creating a new directory and mounting the EFS file system </h2>

1. In SSH session, make a new directory by typing sudo mkdir efs
2. Back in the AWS Management Console, on the Services menu, choose EFS.
3. Choose My First EFS File System
4. In the Amazon EFS Console, on the top right corner of the page, choose Attach to open the Amazon EC2 mount instructions.
5. Copy the entire command in the Using the NFS client section.
6. In your Linux SSH session, mount your Amazon EFS file system by:
     - Pasting the command
     - Pressing ENTER
7. Get a full summary of the available and used disk space usage by entering:
     - sudo df -hT

<p align="center">
<br/>
<img src="https://i.imgur.com/0kTMuIS.png"/>

<h2>Task 5: Examining the performance behavior of your new EFS file system </h2>

1. Examine the write performance characteristics of your file system by entering:
        - "sudo fio --name=fio-efs --filesize=10G --filename=./efs/fio-efs-test.img --bs=1M --nrfiles=1 --direct=1 --sync=0 --rw=write --iodepth=200 --ioengine=libaio"

<h2> Monitoring performance by using Amazon CloudWatch </h2>

1. In the AWS Management Console, on the Services menu, choose CloudWatch.
2. In the navigation pane on the left, choose Metrics.
3. In the All metrics tab, choose EFS.
4. Choose File System Metrics.
5. Select the row that has the PermittedThroughput Metric Name.
6. On the graph, choose and drag around the data line. If you do not see the line graph, adjust the time range of the graph to display the period during which you ran the fio command.
7. Pause your pointer on the data line in the graph. The value should be 105M.
8. In the All metrics tab, uncheck the box for PermittedThroughput.
9. Select the check box for DataWriteIOBytes.
10. If you do not see DataWriteIOBytes in the list of metrics, use the File System Metrics search to find it.
11. Choose the Graphed metrics tab.
12. On the Statistics column, select Sum.
13. On the Period column, select 1 Minute.
14. Pause your pointer on the peak of the line graph. Take this number (in bytes) and divide it by the duration in seconds (60 seconds). The result gives you the write throughput (B/s) of your file system during your test.

Congratulations! You created an EFS file system, mounted it to an EC2 instance, and ran an I/O benchmark test to examine its performance characteristics.

<p align="center">
<br/>
<img src="https://i.imgur.com/a0rUxJV.png"/>

