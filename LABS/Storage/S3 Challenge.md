📦 AWS S3 Challenge Lab

This lab teaches you how to work with Amazon S3 securely and efficiently.
You will practice bucket creation, object storage, permissions, versioning, and encryption while facing real-world challenges.

🎯 Lab Objectives

By the end of this lab, you will be able to:

Create and configure S3 buckets

Upload, download, and manage objects

Set bucket policies and IAM permissions

Enable versioning and server-side encryption

Enable logging and monitoring

Implement S3 lifecycle rules

Troubleshoot common S3 issues

🛠️ Lab Steps
1️⃣ Create an S3 Bucket

Open S3 Console → Create bucket

Configure:

Bucket name: my-challenge-bucket-<yourname>

Region: Choose a nearby region

Block all public access: Enabled (for security)

Versioning: Disabled (we will enable later)

Default encryption: None (we will enable later)

Click Create bucket

2️⃣ Upload Objects to the Bucket

Upload 3 sample files: text, image, and JSON

Test downloading the files from the console

Use AWS CLI to upload:

aws s3 cp sample.txt s3://my-challenge-bucket-<yourname>/

3️⃣ Configure Bucket Versioning

Open bucket → Properties → Versioning

Enable Versioning

Upload a file with the same name (sample.txt) twice.

Check the versions tab → two versions appear

Test restoring the previous version.

4️⃣ Enable Server-Side Encryption

Open bucket → Properties → Default encryption

Choose SSE-S3 or SSE-KMS

Upload a new file and verify encryption:

aws s3api head-object --bucket my-challenge-bucket-<yourname> --key newfile.txt


Check for "ServerSideEncryption": "AES256" or "aws:kms"

5️⃣ Configure Bucket Policies & Permissions

Go to Permissions → Bucket Policy

Example: allow read-only access for a specific IAM user:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {"AWS": "arn:aws:iam::<account-id>:user/TestUser"},
      "Action": ["s3:GetObject"],
      "Resource": ["arn:aws:s3:::my-challenge-bucket-<yourname>/*"]
    }
  ]
}


Test by logging in as the IAM user.

6️⃣ Enable Logging & Monitoring

Server access logs:

Permissions → Logging → Enable

Create a logging bucket (e.g., my-challenge-logs)

Enable logs to be sent there

CloudWatch Metrics:

Enable Request metrics

Observe number of GET, PUT, DELETE requests

7️⃣ Implement Lifecycle Rules

Open bucket → Management → Lifecycle rules

Create a rule:

Move files older than 30 days to Glacier

Delete files older than 365 days

Test by uploading files and observing simulated transitions.

8️⃣ Test S3 Security

Try public access by entering file URL in browser → ❌ should fail

Try IAM user without permission → ❌ access denied

Try encrypted file download → ✅ works with permission

🎓 Takeaways

Learned how to manage S3 buckets and objects

Enabled versioning to protect against accidental deletion

Configured encryption at rest

Applied bucket policies to enforce least privilege

Used logging, monitoring, and lifecycle rules for compliance

Observed effects of security misconfigurations

⚠️ Challenges Encountered
Challenge	Description
Upload blocked	Bucket policy denied upload
Public file access	Public access block not enabled
Encryption misconfigured	SSE-KMS key missing permissions
Old files not archived	Lifecycle rules not configured correctly
IAM user access denied	User not in policy or lacked S3 actions
🧩 Solutions

✔ Check bucket policy and IAM permissions
✔ Enable Block Public Access to prevent accidental exposure
✔ Verify KMS key permissions for encryption
✔ Test lifecycle rules with temporary files before production
✔ Use CloudTrail / CloudWatch to audit access
<img width="1354" height="547" alt="iyo eza kqala" src="https://github.com/user-attachments/assets/54bf0b6f-68c1-4aa0-bd7b-3641b5f398b5" />
<img width="1348" height="547" alt="Screenshot 2025-11-27 151024 khona eza kuqala" src="https://github.com/user-attachments/assets/13e070f0-ce76-47e2-ba43-38752f8ee63a" />
<img width="1354" height="546" alt="website easy made" src="https://github.com/user-attachments/assets/422202b3-b290-4e58-820d-64a9cb814464" />
<img width="1348" height="544" alt="Screenshot 2025-11-27 150903" src="https://github.com/user-attachments/assets/25283ea9-ae44-477a-86a1-64aea3fb5f7b" />
<img width="1366" height="162" alt="Screenshot 2025-11-27 150835" src="https://github.com/user-attachments/assets/f82389a3-01e5-4826-9019-0aad1499c6f1" />
<img width="1347" height="562" alt="Screenshot 2025-11-27 150816" src="https://github.com/user-attachments/assets/4ba0053a-65eb-491c-ab05-2ac60f3ee69b" />
<img width="1342" height="538" alt="Screenshot 2025-11-27 150741" src="https://github.com/user-attachments/assets/f99dd654-6a24-4cc6-988b-39c1d9ab5bc9" />
<img width="1351" height="534" alt="Screenshot 2025-11-27 150716" src="https://github.com/user-attachments/assets/e68f7c01-f308-4a8b-99a8-8761488251c0" />
<img width="1356" height="210" alt="Screenshot 2025-11-27 150516" src="https://github.com/user-attachments/assets/1ab0f3ce-6c7e-4276-bbcf-d28f39dccb5a" />
<img width="1366" height="560" alt="Screenshot 2025-11-27 150453" src="https://github.com/user-attachments/assets/c0444aaf-9756-425f-8202-36e40e9f812f" />
<img width="1342" height="557" alt="Screenshot 2025-11-27 150422" src="https://github.com/user-attachments/assets/935dbb76-4eb1-4c09-bb55-f5a90b526ba8" />
<img width="1366" height="220" alt="Screenshot 2025-11-27 150247" src="https://github.com/user-attachments/assets/073d89eb-33a6-43e9-bcae-fddf8eca1ddb" />
<img width="1342" height="545" alt="Screenshot 2025-11-27 150214" src="https://github.com/user-attachments/assets/a1859204-fdf5-4dd7-b07d-c2748c9476c1" />
<img width="1366" height="679" alt="Screenshot 2025-11-27 150017" src="https://github.com/user-attachments/assets/1adb438a-fff8-4128-b635-70715baa49bf" />
<img width="1326" height="557" alt="Screenshot 2025-11-27 145710" src="https://github.com/user-attachments/assets/47756ae5-2122-4660-9c73-784bb68f7e17" />
<img width="1366" height="547" alt="Screenshot 2025-11-27 145601" src="https://github.com/user-attachments/assets/07e3a3fd-214d-477d-97e9-4ab83b2b7b0f" />
<img width="1353" height="463" alt="Screenshot 2025-11-27 145140" src="https://github.com/user-attachments/assets/1871d39f-443f-4d47-83f5-25d1d7b79fe8" />
<img width="1333" height="316" alt="Screenshot (26)" src="https://github.com/user-attachments/assets/41a8d4fe-c354-4fb2-b948-b050abcd98ee" />
<img width="1093" height="512" alt="Screenshot (25)" src="https://github.com/user-attachments/assets/02b1e02b-8832-456d-b5f1-7e0436d4b2b5" />
<img width="1308" height="540" alt="Screenshot (24)" src="https://github.com/user-attachments/assets/25a13d45-84a8-44d1-ba89-ffd2383c9e98" />
<img width="1087" height="236" alt="Screenshot (23)" src="https://github.com/user-attachments/assets/5730385d-55af-4372-8a3e-6355bff810da" />
<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/7c14a6dc-8a3a-44a1-be4d-4ae9c1fcffe0" />


