# Jenkins Maven Integration on Linux

## Aim
To install Java, Maven, and Jenkins on Linux/Ubuntu and build a Maven project using Jenkins.

---

# Prerequisites

- Ubuntu/Linux system
- Internet connection
- GitHub account
- Sudo access

---

# Step 1: Update System and Install Java

```bash
sudo apt update
sudo apt install openjdk-21-jdk -y
```

Verify Java installation:

```bash
java -version
```

---

# Step 2: Install Maven

Download Maven:

```bash
wget https://archive.apache.org/dist/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz
```

Extract Maven:

```bash
sudo tar -xzf apache-maven-3.9.6-bin.tar.gz -C /opt/
```

Set Maven environment variable:

```bash
echo 'export PATH=/opt/apache-maven-3.9.6/bin:$PATH' | sudo tee /etc/profile.d/maven.sh
```

Apply changes:

```bash
source /etc/profile.d/maven.sh
```

Verify Maven installation:

```bash
mvn -version
```

---

# Step 3: Install Jenkins

Install Jenkins:

```bash
sudo apt install jenkins -y
```

---

# Step 4: Start and Enable Jenkins

Start Jenkins service:

```bash
sudo systemctl start jenkins
```

Enable Jenkins on boot:

```bash
sudo systemctl enable jenkins
```

Check Jenkins status:

```bash
sudo systemctl status jenkins
```

Alternative commands:

```bash
sudo service jenkins start
sudo service jenkins status
```

---

# Step 5: Get Jenkins Admin Password

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Copy the displayed password.

---

# Step 6: Access Jenkins Web Interface

Allow port 8080 in firewall/security groups.

Open browser:

```text
http://<your-public-ip>:8080
```

Example:

```text
http://192.168.1.10:8080
```

Paste the admin password.

---

# Step 7: Configure Maven in Jenkins

1. Open Jenkins Dashboard

2. Go to:

```text
Manage Jenkins → Plugins
```

3. Install:

```text
Maven Integration Plugin
```

4. Go to:

```text
Manage Jenkins → Tools
```

5. Add Maven configuration:

```text
Name: Maven 3.9.6
```

6. Uncheck:

```text
Install Automatically
```

7. Maven Home:

```text
/opt/apache-maven-3.9.6
```

8. Click Save

---

# Step 8: Create Jenkins Freestyle Job

1. Click:

```text
New Item
```

2. Enter job name

3. Select:

```text
Freestyle Project
```

4. Under Source Code Management:
   - Select Git
   - Enter GitHub repository URL

Example:

```text
https://github.com/mvsanthi123/
```

5. Under Build Steps:
   - Select:

```text
Invoke top-level Maven targets
```

6. Select Maven Version:

```text
Maven 3.9.6
```

7. Goals:

```text
clean install
```

8. Click Save

---

# Step 9: Run the Build

Click:

```text
Build Now
```

Jenkins will:
- Download dependencies
- Compile the project
- Create JAR file

---

# Step 10: Verify Generated JAR File

Switch to Jenkins user:

```bash
sudo su - jenkins
```

Navigate to generated JAR location:

```bash
cd /var/lib/jenkins/.m2/repository/com/mycompany/app/my-app/1.0-SNAPSHOT/
```

Check files:

```bash
ls
```

Run the JAR file:

```bash
java -jar my-app-1.0-SNAPSHOT.jar
```

Expected Output:

```text
Hello world
```

---

# Outcome

- Java installed successfully
- Maven installed successfully
- Jenkins installed successfully
- Maven project built using Jenkins
- JAR file generated and executed successfully