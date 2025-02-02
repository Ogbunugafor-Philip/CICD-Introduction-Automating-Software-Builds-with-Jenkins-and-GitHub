# CICD-Introduction-Automating-Software-Builds-with-Jenkins-and-GitHub


## Introduction

This project establishes a comprehensive and automated Continuous Integration/Continuous Deployment (CI/CD) pipeline by integrating Jenkins with GitHub. The core objective is to streamline the software development lifecycle, from code commit to deployment, by automating the build, test, and deployment processes triggered by code changes pushed to a GitHub repository. This automation minimizes manual intervention, accelerates feedback loops, enhances code quality, and ultimately facilitates faster and more reliable software releases.

## Project Objectives

*   Automate the software build and test process triggered by code changes.
*   Implement continuous integration of code changes through automated builds and tests.
*   Enable continuous delivery or deployment of software to target environments.

## Project Implementation

### Jenkins Server Setup

Jenkins is an open-source automation server used for continuous integration and continuous delivery (CI/CD) to automate software development processes.

1.  **SSH into the Jenkins server:**

    ```bash
    ssh -i <path-to-your-private-key.pem> user@serverIP
    ```

2.  **Update the Jenkins Server:**

    ```bash
    sudo apt update
    ```

3.  **Install Java:**

    ```bash
    sudo apt install openjdk-17-jre
    ```

4.  **Install Jenkins:**

    ```bash
    sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
    [https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key](https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key)

    echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
    [https://pkg.jenkins.io/debian-stable](https://pkg.jenkins.io/debian-stable) binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null

    sudo apt-get update

    sudo apt-get install jenkins
    ```

5.  **Check Jenkins Server Status:**

    ```bash
    sudo systemctl status jenkins
    ```

6.  **Access Jenkins in the Browser:**

    Open port 8080 in your AWS Management Console's security group inbound rules (TCP 8080, limit source IP for security).  Then access Jenkins via: `http://<server_IP>:8080`

7.  **Get the Administrative Password:**

    ```bash
    sudo cat /var/lib/jenkins/secrets/initialAdminPassword
    ```

8.  **Initial Jenkins Setup:**

    *   Enter the admin password.
    *   Install suggested plugins.
    *   Create the first admin user.

9.  **Create a Jenkins Job:**

    *   Click "New Item".
    *   Enter a name and select "Freestyle project".
    *   Click "OK".

10. **Configure the Jenkins Job:**

    *   Under "Source Code Management", select "Git".
    *   Enter your GitHub repository URL.
    *   Specify the branch (e.g., `main`).
    *   Under "Build Triggers", select "GitHub hook trigger for GITScm polling".
    *   Save the configuration.

11. **Configure GitHub Webhook:**

    *   In your GitHub repository, go to "Settings" -> "Webhooks" -> "Add webhook".
    *   Set the "Payload URL" to `http://<server_IP>:8080/github-webhook/` (Note: Update the IP address if your EC2 instance restarts).
    *   Select "Let me select individual events" and choose "Pull requests" and "Pushes".
    *   Add the webhook.

12. **Test the Pipeline:**

    *   Go back to the Jenkins project dashboard and click the "Play" button to build.
    *   Verify the build is successful.

## Conclusion

This project successfully established a robust CI/CD pipeline using Jenkins and GitHub webhooks. By automating the build, test, and deployment processes, we have significantly improved development efficiency, reduced manual errors, and accelerated feedback loops. This implementation enables faster and more reliable software releases, contributing to higher quality software and increased team productivity. The automated pipeline provides a solid foundation for future enhancements, such as integrating additional testing stages, expanding deployment targets, and further optimizing the software delivery process.
