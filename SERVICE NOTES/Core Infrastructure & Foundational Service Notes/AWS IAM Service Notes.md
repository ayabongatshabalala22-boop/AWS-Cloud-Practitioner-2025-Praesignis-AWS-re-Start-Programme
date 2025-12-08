# AWS IAM (Identity and Access Management) Service Notes

IAM is a foundational AWS service that securely controls access to AWS services and resources.  
It answers the question: **"Who can do what, and under what conditions?"**

---

## 1. Core Concepts & Terminology

- **Users**: Represents a person or application that interacts with AWS.
- **Groups**: A collection of users. Policies are attached to groups rather than individual users to simplify management (e.g., Developers, Admins, Auditors).
- **Policies**: JSON documents that define permissions. They are the core of IAM and can be attached to users, groups, roles, or resources.
- **Roles**: IAM entities that grant temporary permissions. Assumed by AWS services (e.g., EC2 needing S3 access) or by users for cross‑account access. Roles do not have credentials until assumed.
- **Permissions Boundary**: Advanced IAM feature used to delegate administration of a subset of users/roles while ensuring those entities cannot exceed a maximum set of permissions.

---

## 2. Policy Structure (JSON)

IAM policies use a specific JSON structure to define rules:

| Element     | Description                                   | Values/Examples                          |
|-------------|-----------------------------------------------|------------------------------------------|
| **Version** | Policy language version                       | `2012-10-17` (current standard)          |
| **Statement** | Main block containing the rule              | Array of objects                         |
| **Effect**  | Whether the statement allows or denies access | `Allow` or `Deny`                        |
| **Action**  | Specific AWS API calls permitted/denied       | `s3:GetObject`, `ec2:RunInstances`, `*`  |
| **Resource**| AWS resource the action applies to            | `arn:aws:s3:::mybucket/*`, `*`           |
| **Condition** | (Optional) Constraints on when policy applies | Source IP, time of day, etc.            |

**Example Policy Snippet:**

```json
{
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::my_data_bucket"
}
