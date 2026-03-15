# Linux-administration-ii
# Linux Administration II — Advanced Permissions & ACL Configuration

This project builds on foundational Linux administration skills by introducing **advanced permissions**, **Access Control Lists (ACLs)**, and **practical permission testing**.  
All work was performed on Ubuntu in a controlled lab environment and documented with screenshots.

Before beginning the project, Wi‑Fi drivers were installed and verified to ensure a stable working environment.

---

# 📡 Prerequisite: Wi‑Fi Driver Installation

Before starting Linux Administration II, Wi‑Fi drivers were installed and confirmed working.

### Screenshots:
![WiFi Confirmation 1](screenshots/01-wifi-confirmation.png)  
![WiFi Confirmation 2](screenshots/02-wifi-confirmation.png)  
![WiFi Confirmation 3](screenshots/03-wifi-confirmation.png)

---

# 🧩 Project Objectives

- Create structured project directories  
- Manage users and groups  
- Apply advanced Linux permissions  
- Configure Access Control Lists (ACLs)  
- Test and validate permission boundaries  
- Document the entire workflow for portfolio presentation  

---

# 🟦 Step 1 — Create Project Directories

Two directories were created to simulate separate project spaces.

### Commands:
```bash
sudo mkdir -p /admin2/projectA
sudo mkdir -p /admin2/projectB
ls -l /admin2
```

### Screenshot:
![Step 1](screenshots/04-create-directories.png)

---

# 🟩 Step 2 — Create Users and Group

Two users and one group were created for permission testing.

### Commands:
```bash
sudo adduser usera
sudo adduser userb
sudo groupadd admin2group
```

Add both users to the group:
```bash
sudo usermod -aG admin2group usera
sudo usermod -aG admin2group userb
```

### Screenshot:
![Step 2](screenshots/05-create-users.png)

---

# 🟦 Step 3 — Verify Group Membership

Confirm both users were successfully added to the group.

### Commands:
```bash
groups usera
groups userb
```

### Screenshot:
![Step 3](screenshots/06-group-membership.png)

---

# 🟩 Step 4 — Assign Group Ownership

The project directories were assigned to the new group.

### Commands:
```bash
sudo chown :admin2group /admin2/projectA
sudo chown :admin2group /admin2/projectB
ls -l /admin2
```

### Screenshot:
![Step 4](screenshots/07-chown.png)

---

# 🟦 Step 5 — Apply Advanced Permissions

Permissions were set to allow full access for owner and group, and no access for others.

### Commands:
```bash
sudo chmod 770 /admin2/projectA
sudo chmod 770 /admin2/projectB
ls -ld /admin2/projectA
```

### Screenshot:
![Step 5](screenshots/08-chmod.png)

---

# 🟩 Step 6 — Configure ACLs

ACLs were applied to give users different access levels.

### Commands:

Give **usera** full access:
```bash
sudo setfacl -m u:usera:rwx /admin2/projectA
```

Give **userb** read-only access:
```bash
sudo setfacl -m u:userb:r-x /admin2/projectA
```

Verify ACLs:
```bash
getfacl /admin2/projectA
```

### Screenshot:
![Step 6](screenshots/09-setfacl.png)

---

# 🟦 Step 7 — Permission Testing & Final Verification

### Test as usera (should succeed):
```bash
su - usera
cd /admin2/projectA
touch testA.txt
```

### Test as userb (write should fail, read should succeed):
```bash
su - userb
cd /admin2/projectA
touch testB.txt   # expected to fail
cat testA.txt     # expected to succeed
```

### Final verification:
```bash
ls -l /admin2/projectA
getfacl /admin2/projectA
```

### Screenshot:
![Step 7](screenshots/10-final-verification.png)

---

# 🧠 Skills Demonstrated

| Skill Area | Description |
|-----------|-------------|
| **User & Group Management** | Creating and managing Linux accounts |
| **Filesystem Permissions** | Applying chmod, chown, and directory controls |
| **ACL Configuration** | Using setfacl/getfacl for fine‑grained access |
| **Security Best Practices** | Implementing least‑privilege access |
| **Troubleshooting** | Testing and validating permission boundaries |
| **Documentation** | Clean, structured, professional project documentation |

---

# 📘 What I Learned

- How to structure Linux directories for multi‑user environments  
- How to apply advanced permissions beyond basic chmod  
- How ACLs provide granular access control  
- How to test and validate user access in real scenarios  
- How to document Linux administration work for a professional portfolio  

---

# 🏁 Summary

Linux Administration II demonstrates the ability to configure and verify advanced Linux permissions using both traditional permission models and ACLs.  
This project reflects real‑world IT support and system administration tasks and is a strong addition to a technical portfolio.
