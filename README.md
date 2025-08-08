# 📦 Continuous Integration for a Node.js Web Application using Git, Jenkins, and AWS Elastic Beanstalk
   ## 💻 (NIC Internship)

This project was done to demonstrates Continuous Integration (CI) pipeline using Jenkins and AWS Elastic Beanstalk for deployment of a Node.js based web application
---

## 🏢 Workflow

1. **AWS Account creation**  
2. **EC2 started and connect**  
3. **Java installed on EC2**  
4. **Jenkins installed**  
5. **Went to Instance security groups and edited inbound rules**  
   - Added port **8080** with custom IP range to access Jenkins from browser
   - Installed node and zip in my ec2 machine
6. **Created and configured Elastic Beanstalk application in aws for deploying my nodejs application.**
7. **Setup Jenkins with plugins**  
   - Then setup Credentials with access key and secret access key of an IAM, in **Jenkins → Credentials** 
   -(Now Jenkins agent can securely and programmatically talk to AWS) 
8. **Job creation in Jenkins via Pipeline option**  
9. **GitHub project link attached**  
10. **Clicking on Build Now lets triggered Jenkins pipeline pull latest code and run each stages**  
11. **Visited Elastic Beanstalk environment and opened the provided url to reach the website i.e our App**

---

## 💻 How to Run

# 🙇‍♂️🙇‍♂️ Sorry, I have closed the instances to avoid AWS cost  
Therefore, the application is inaccessible right now. Although you can go through my git files suitable to be deployed via Jenkins
