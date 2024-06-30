# Simple Elastic SIEM Lab 

## Objective

I learned how to set up a home lab for Elastic Stack Security Information and Event Management (SIEM) using the Elastic Web portal and a Kali Linux VM. I also learned how to generate security events on the Kali VM, set up an agent to forward data to the SIEM, and query and analyze the logs in the SIEM.

### Skills Learned

- Set up a free Elastic account.
- Install the Kali VM.
- Configure the Elastic Agent on the Linux VM to collect the logs and forward it to the SIEM.
- Generate security events on the Kali VM.
- Query to find the security events in the Elastic SIEM.
- Create a Dashboard to visualize security events.
- Create alerts for security events.
- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Nmap) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps
Before getting started, I created a free account to set up a cloud Elastic instance that I can run the SIEM on.
I also installed VirtualBox on my PC.

Task 1: Set up an Elastic Account

   1. Sign up for a free trial to use Elastic Cloud at <a href="https://cloud.elastic.co/registration">Elastic.com</a>
   2. Once you have an Elastic account, log in to the Elastic Cloud console at <a href="https://cloud.elastic.co.">Elastic.com</a>
   3. Click on “Start your free trial.”
   4. Click on the “Create Deployment” button and select “Elasticsearch” as the deployment type.
   5. Choose a region and deployment size that fits your needs and click on “Create Deployment.”
   6. Wait for the configuration to complete.
   7. Once the deployment is ready, click “continue.”


Task 2: Setting up the Linux VM

Next, we need to set up the Linux VM. You can use any Linux OS and virtualization software for this, but I used Kali Linux and Oracle VirtualBox.

To set it up, follow these steps:

    Download the Kali Linux VM from the official Kali website at <a href="https://kali.org">Kali.com</a>
    Create a new VM with the Kali VM file in your preferred virtualization platform, such as VirtualBox or VMware.
    Start the VM and follow the on-screen prompts to install Kali.
    Once the installation is complete, log in to the Kali VM using the credentials “kali” for both the username and password.
