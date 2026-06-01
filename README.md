# AWS IAM Enumeration with Pacu

**Author:** Chandru Ganesan

## Overview

This lab demonstrates AWS Identity and Access Management (IAM) enumeration using Pacu, an AWS exploitation framework developed by Rhino Security Labs.

The objective was to identify IAM users, groups, roles, and permissions that could reveal potential security weaknesses, excessive privileges, or privilege escalation opportunities.

## Tools Used

- Pacu
- AWS IAM
- AWS CLI
- Kali Linux

## Objectives

- Authenticate to AWS using IAM credentials
- Enumerate IAM permissions
- Discover IAM users, groups, and roles
- Analyze IAM configurations and privileges

---

## Step 1: Import AWS Credentials

### Method 1: Directly in Pacu

```bash
new_session cybr-iam-lab
set_keys
whoami
```

### Method 2: Import AWS CLI Profile

```bash
aws configure --profile cybr

import_keys cybr
whoami
```

---

## Step 2: IAM Enumeration

Search for IAM modules:

```bash
search iam
```

Relevant modules:

- iam__enum_permissions
- iam__enum_users_roles_policies_groups

### Enumerate Permissions

```bash
run iam__enum_permissions
```

Result:

- Approximately 20 permissions discovered

### Enumerate IAM Entities

```bash
run iam__enum_users_roles_policies_groups
```

Result:

| Resource | Count |
|-----------|--------|
| Users | 4 |
| Roles | 19 |
| Groups | 2 |
| Policies | 0 |

Users Discovered:

- Chris
- Joel
- Mary
- Mike

Groups Discovered:

- Developers
- Infrastructure

---

## Step 3: Review Stored IAM Data

```bash
data iam
```

Discovered:

- IAM Users
- IAM Groups
- IAM Roles
- Service-linked Roles
- AWS SSO Roles
- CloudFormation StackSets Roles
- Custom Support Roles

---

## Step 4: Review Current User Access

```bash
whoami
```

Findings:

- Group Membership: Developers
- Attached Policy: AllowEnumerateRoles

---

## Security Observations

- Enumeration revealed multiple IAM users and roles.
- Service-linked roles exposed active AWS services.
- IAM role trust relationships should be reviewed for privilege escalation risks.
- Even limited IAM permissions can provide valuable reconnaissance information.

---

## Key Takeaways

- Pacu is an effective framework for AWS IAM reconnaissance.
- IAM enumeration is often the first step in AWS security assessments.
- Understanding users, groups, roles, and permissions helps identify potential attack paths.

## References

- https://github.com/RhinoSecurityLabs/pacu
- https://aws.amazon.com/iam/
- https://cybr.com
