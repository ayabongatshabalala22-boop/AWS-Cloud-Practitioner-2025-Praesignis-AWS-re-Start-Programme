💽 AWS Lab: Working with Amazon EBS

This lab teaches you how to create, attach, and manage Amazon Elastic Block Store (EBS) volumes.
You will practice creating volumes, attaching them to EC2 instances, resizing, and snapshotting.

🎯 Lab Objectives

By the end of this lab, you will be able to:

Create EBS volumes in AWS

Attach volumes to EC2 instances

Format and mount volumes on Linux

Resize and extend volumes

Create and restore snapshots

Delete volumes safely

Understand EBS volume types and use cases

🛠️ Lab Steps
1️⃣ Launch an EC2 Instance

Open EC2 Console → Launch Instance

Choose Amazon Linux 2 (or Ubuntu)

Network: choose a VPC and subnet

Security Group: allow SSH from your IP

Launch instance and note its Instance ID

2️⃣ Create an EBS Volume

Go to EC2 → Elastic Block Store → Volumes → Create Volume

Configure:

Volume Type: General Purpose SSD (gp3)

Size: 10 GB

Availability Zone: same as your EC2 instance

Encrypted: Enabled (optional but recommended)

Click Create Volume

3️⃣ Attach EBS Volume to EC2

Select the new volume → Actions → Attach Volume

Select your EC2 instance → Device: /dev/sdf (Linux)

4️⃣ Format and Mount Volume (Linux)

SSH into your EC2 instance:

# List disks
lsblk

# Format the volume
sudo mkfs -t xfs /dev/xvdf

# Create mount point
sudo mkdir /mnt/ebs

# Mount the volume
sudo mount /dev/xvdf /mnt/ebs

# Verify mount
df -h

5️⃣ Make Mount Persistent (Optional)

Edit /etc/fstab:

sudo nano /etc/fstab


Add:

/dev/xvdf   /mnt/ebs   xfs   defaults,nofail   0   2


Test:

sudo umount /mnt/ebs
sudo mount -a
df -h

6️⃣ Create a Snapshot

Go to EC2 → Volumes → Select your volume → Create Snapshot

Name: ebs-lab-snapshot

Click Create Snapshot

Snapshots can be restored into new volumes in same or different AZ

7️⃣ Resize EBS Volume

Select the volume → Actions → Modify Volume

Increase size (e.g., 10 GB → 20 GB)

SSH into EC2 and expand filesystem:

# For XFS
sudo xfs_growfs /mnt/ebs

# For ext4
sudo resize2fs /dev/xvdf


Verify new space:

df -h

8️⃣ Delete Volume (Cleanup)

Unmount volume:

sudo umount /mnt/ebs


Go to EC2 → Volumes → Actions → Delete Volume

Confirm deletion

🎓 Takeaways

EBS volumes provide persistent block storage for EC2

You can create, attach, format, mount, and resize volumes easily

Snapshots allow backup and restore of data

Encrypted volumes secure data at rest

Mounting and fstab configuration ensures persistence

⚠️ Challenges Encountered
Challenge	Description
Volume not in same AZ	Cannot attach EBS volume across AZs
Device name mismatch	Linux /dev/sdf appears as /dev/xvdf
Filesystem not expanded	After resize, forgot xfs_growfs
Snapshot restore in different AZ	Need to create new volume in correct AZ
🧩 Solutions

✔ Always create EBS in same Availability Zone as EC2
✔ Use lsblk to check device names
✔ Run xfs_growfs or resize2fs after volume expansion
✔ Restore snapshots by creating new volumes in target AZ
<img width="1366" height="290" alt="lab-1 (1)" src="https://github.com/user-attachments/assets/3865b786-27c1-4627-b498-3afe38265251" />
<img width="1366" height="460" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/ce923de4-1474-4227-a296-ff9d989bec3c" />

<img width="711" height="543" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/2d589eaf-bd0b-4692-adab-ff10ae871075" />
<img width="1366" height="515" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/abcaf8ac-dad7-4c62-9b20-6bae525ae885" />

<img width="1366" height="515" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/b5ad8fd1-4bab-416a-8638-f74695cf21d5" />



<img width="1314" height="530" alt="Screenshot (7)" src="https://github.com/user-attachments/assets/cc7ac00c-ec5a-4414-8b43-9c51f348f7b5" />
<img width="1103" height="233" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/cf514b14-ed8f-415c-bc3f-b52da841c454" />
<img width="1307" height="554" alt="Screenshot (9)" src="https://github.com/user-attachments/assets/7f75daef-8cc1-48eb-b435-92a3d3e413eb" />
<img width="1291" height="274" alt="Screenshot (10)" src="https://github.com/user-attachments/assets/13cfe2c2-4f04-4b01-a4c6-49db7801a1cd" />
<img width="1337" height="401" alt="Screenshot (11)" src="https://github.com/user-attachments/assets/4e6cad70-4b9a-482c-883c-7ca763c15806" />
<img width="1339" height="393" alt="Screenshot (12)" src="https://github.com/user-attachments/assets/69e4cf05-d76f-4457-9f55-78e5d465a50c" />
<img width="1335" height="156" alt="Screenshot (13)" src="https://github.com/user-attachments/assets/472c2566-888b-49c2-98db-7804704220f7" />
<img width="1331" height="287" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/283a1c55-d692-40bc-b916-684860f46136" />
<img width="1348" height="551" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/194ca9ea-9384-4b36-886e-fa4e4b06c7f5" />
<img width="1095" height="293" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/63171382-904d-486c-b688-fefb86800d58" />
<img width="1107" height="159" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/23596992-34bc-4086-830a-00917fb36e54" />
<img width="1336" height="226" alt="Screenshot (18) - Copy" src="https://github.com/user-attachments/assets/dd25bb56-5f0e-4ea9-9cbd-44417231ab70" />
<img width="1336" height="494" alt="Screenshot (18)" src="https://github.com/user-attachments/assets/f6fa9eda-48e0-4489-90b3-a7edf1ebfd03" />
<img width="1311" height="543" alt="Screenshot (19)" src="https://github.com/user-attachments/assets/a0650b4d-a545-4aca-9f6e-86baba369cbc" />
<img width="1109" height="201" alt="Screenshot (20)" src="https://github.com/user-attachments/assets/99ca28a9-3bfc-4bab-acee-bd661d6aec61" />
<img width="1318" height="509" alt="Screenshot (21)" src="https://github.com/user-attachments/assets/f88a157d-c88b-4131-b0ae-fbaed479e9c2" />
<img width="1094" height="252" alt="Screenshot (22)" src="https://github.com/user-attachments/assets/9c80d0c2-7bc5-46ea-a40f-656ee5b6a4ee" />
