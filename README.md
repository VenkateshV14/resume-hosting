# Automated Resume Deployment with Jenkins & Tomcat

## 📌 Project Overview
This project sets up and configures a **Jenkins server** to automate the deployment of my resume on a **Tomcat server**. Both servers are hosted on **AWS EC2 instances**. The pipeline ensures that whenever changes are pushed to the GitHub repository, Jenkins triggers an automated deployment to update the resume on the Tomcat server using a **Maven Project**.

## 🚀 Features
- **Automated CI/CD Pipeline**: Configured with Jenkins to deploy updates automatically.
- **AWS EC2 Hosted**: Both Jenkins and Tomcat servers are running on AWS instances.
- **GitHub Integration**: Triggers deployment whenever changes are pushed to the repository.
- **Maven-Based Deployment**: Utilizes **Maven Project** in Jenkins for build and deployment.
- **Tomcat Server Deployment**: The resume is served via a Tomcat application server.

## 🛠️ Technologies Used
- **AWS EC2** (for hosting Jenkins & Tomcat)
- **Jenkins** (for CI/CD automation)
- **Apache Tomcat** (to serve the deployed resume)
- **Maven** (for build automation)
- **GitHub** (for version control & integration)
- **Shell Scripting** (for automation)

## 🔧 Setup & Configuration

### 1️⃣ **Launch EC2 Instances**
- Create two AWS EC2 instances: one for Jenkins, another for Tomcat.

### 2️⃣ **Install & Configure Jenkins**
```sh
# Install Java (required for Jenkins & Tomcat)
sudo apt update && sudo apt install openjdk-17-jdk -y
sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo yum upgrade
# Add required dependencies for the jenkins package
sudo yum install fontconfig java-17-openjdk
sudo yum install jenkins
sudo systemctl daemon-reload
# Add Jenkins repository & install Jenkins
wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io.key
sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update && sudo apt install jenkins -y

# Start and enable Jenkins service
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

### 3️⃣ **Install & Configure Tomcat**
```sh
# Install Tomcat
sudo apt update && sudo apt install tomcat9 -y

# Start and enable Tomcat
sudo systemctl start tomcat9
sudo systemctl enable tomcat9
```

### 4️⃣ **Configure Jenkins for GitHub Integration**
- Install **GitHub Plugin** and **Maven Integration Plugin** in Jenkins.
- Add **GitHub Webhook** to trigger builds.
- Configure **Jenkins Maven Project** to build and deploy the resume.

### 5️⃣ **Automate Deployment with Jenkins Maven Project**
- In **Jenkins**, create a new **Maven Project**.
- Link it to your **GitHub repository**.
- Configure the **Build Step** to execute Maven commands:

```sh
clean package
```

- Add a **Post-Build Step** to deploy the generated WAR file to Tomcat:

## 🔥 How It Works
1. Push updates to the GitHub repository.
2. Poll SCM notifies Jenkins.
3. Jenkins fetches the latest code and runs the Maven build.
4. The generated WAR file is deployed to the Tomcat server.
5. The resume is automatically updated on the server.

## 📂 Project Structure
```
/
├── src/
│   ├── main/
│   │   ├── webapp/
│   │   │   ├── index.html  # Resume webpage
│   │   │   ├── style.css   # Stylesheet for resume
│   │   │   ├── pic.jpg     # Profile picture
│   │   │   ├── WEB-INF/
│   │   │   │   ├── web.xml  # Deployment descriptor
│   ├── pom.xml  # Maven build file
├── README.md        # Project documentation
```

## 📢 Future Enhancements
- Add **Dockerized Jenkins & Tomcat** for better scalability.
- Implement **SSL/TLS encryption** for secure communication.
- Integrate **Terraform for Infrastructure as Code (IaC)**.

## 🙌 Connect with Me
- **GitHub**: [VenkateshV14](https://github.com/VenkateshV14)
- **LinkedIn**: [Venkatesh Vakamudula](https://linkedin.com/in/venky-venkatesh)

---
💡 *Feel free to fork, improve, or contribute to this project!* 🚀
