# Access Control & User Management
### **Exercise 1: File Permissions and Ownership**

1. **Create a directory called `access_practice`:**
   ```bash
   mkdir access_practice
   ```

2. **Navigate into the `access_practice` directory:**
   ```bash
   cd access_practice
   ```

3. **Create a file named `secret.txt`:**
   ```bash
   touch secret.txt
   ```

4. **Set the file permissions to allow read and write access for the owner, and no access for group and others:**
   ```bash
   chmod 600 secret.txt
   ```
   - `chmod 600` sets the permissions to `-rw-------`, meaning the owner can read and write, but no one else has any access.

5. **Change the ownership of the file to a different user (replace `otheruser` with the actual username):**
   ```bash
   sudo chown otheruser:otheruser secret.txt
   ```
   - This command changes both the owner and the group to `otheruser`.

6. **Try accessing the file from the original and the different user accounts:**
   - **As the original user:**
     ```bash
     cat secret.txt
     ```
     - You should get a "Permission denied" error.
   - **As the new owner (`otheruser`):**
     ```bash
     su - otheruser
     cd access_practice
     cat secret.txt
     ```
     - The new owner should be able to read and write to the file.

---

### **Exercise 2: User and Group Management**

1. **Create a new user named `user1`:**
   ```bash
   sudo useradd user1
   ```

2. **Create a new group named `group1`:**
   ```bash
   sudo groupadd group1
   ```

3. **Add `user1` to `group1`:**
   ```bash
   sudo usermod -aG group1 user1
   ```
   - The `-aG` flag adds `user1` to `group1` without removing them from other groups.

4. **Change the ownership of `secret.txt` to `user1` and `group1`:**
   ```bash
   sudo chown user1:group1 secret.txt
   ```

5. **Set the file permissions to allow read and write access for the owner and the group:**
   ```bash
   chmod 660 secret.txt
   ```
   - `chmod 660` sets the permissions to `-rw-rw----`, meaning the owner and group can read and write, but others have no access.

6. **Test accessing the file both as `user1` and a different user:**
   - **As `user1`:**
     ```bash
     su - user1
     cd access_practice
     cat secret.txt
     ```
     - `user1` should be able to read and write to the file.
   - **As a different user (not in `group1`):**
     ```bash
     su - differentuser
     cd access_practice
     cat secret.txt
     ```
     - The different user should receive a "Permission denied" error.

---

