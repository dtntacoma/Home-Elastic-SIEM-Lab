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

**Task 1: Set up an Elastic Account**

   1. Sign up for a free trial to use Elastic Cloud at <a href="https://cloud.elastic.co/registration">Elastic.com</a>
   2. Once you have an Elastic account, log in to the Elastic Cloud console at <a href="https://cloud.elastic.co.">Elastic.com</a>
   3. Click on “Start your free trial.”
   4. Click on the “Create Deployment” button and select “Elasticsearch” as the deployment type.
   5. Choose a region and deployment size that fits your needs and click on “Create Deployment.”
   6. Wait for the configuration to complete.
   7. Once the deployment is ready, click “continue.”   

**Task 2: Setting up the Linux VM**

Next, you will need to set up the Linux VM. You can use any Linux OS and virtualization software for this, but I used Kali Linux and Oracle VirtualBox.

To set it up, follow these steps:

   1. Download the Kali Linux VM from the official Kali website at <a href="https://kali.org">kali.org</a>.
   2. Create a new VM with the Kali VM file in your preferred virtualization platform, such as VirtualBox or VMware.
   3. Start the VM and follow the on-screen prompts to install Kali.
   4. Once the installation is complete, log in to the Kali VM using the credentials “kali” for both the username and password.

Note: If you encounter any difficulties with this particular task like I did, you can search for something like this on YouTube: “How to create a virtual machine using VirtualBox/VMware with a Kali VM file.”

**Task 3: Setting up the Agent to Collect Logs**

An agent is a software program that is installed on a device, such as a server or endpoint, to collect and send data to a centralized system for analysis and monitoring. In the context of Elastic SIEM, an agent is used to collect and forward security-related events from your endpoints to your Elastic SIEM instance.

To set up the agent to collect logs from your Kali VM and forward them to your Elastic SIEM instance, follow these steps:

   1. Log in to your Elastic SIEM instance and navigate to the Integrations page by: clicking on the Kibana main menu bar at the top left, then selecting “Integrations” at          the bottom.
  ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/6e2ce7fd-0d91-45d1-bc14-0ef8607b16a4)
   2. Search for “Elastic Defend” and click on it to open the integration page.
  ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/7dd491b9-9c6c-4aae-aedb-6ef36e053312)
   3. Click on “Install Elastic Defend” and follow the instructions provided on the integration page to install the agent on your Kali VM.
      Make sure “Linux” is selected and then copy that command to your clipboard.
   ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/233f8707-61c9-48df-ae6b-fc8aafa609b3)
   ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/507967b6-74c4-4ead-987c-fae1b9d64d50)
   4. Paste that command into the Kali terminal (command line).
   ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/634b4053-af8f-432a-b4cb-e0383a68858b)
   5. Once the agent is installed, which can take a few minutes, you’ll see a message that says “Elastic Agent has been successfully installed.” It will automatically start         collecting and forwarding logs to your Elastic SIEM instance, although it might take a few minutes for the logs to appear in the SIEM.
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/6a83e9c7-4924-4cf6-8a51-394587032b61)
      You can verify that the agent has been installed correctly by running this command: sudo systemctl status elastic-agent.service
    ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/544ddbdd-6e10-4802-9f76-5e090aeedc66)

If you get an error installing the agent, make sure that your Kali is connected to the internet before proceeding by pinging google.com.

**Task 4: Generating Security Events on the Kali VM**

To verify that the agent is working correctly, you can generate some security-related events on your Kali VM. To do this, we can use a tool like Nmap. Nmap (Network Mapper) is a free and open-source utility used for network exploration, management, and security auditing. It is designed to discover hosts and services on a computer network, thus creating a “map” of the network. Nmap can be used to scan hosts for open ports, determine the operating system and software running on the target system, and gather other information about the network.

To run an Nmap scan, follow these steps:

   1. Install Nmap on the Linux VM if you’re not using Kali, Nmap already comes preinstalled in Kali. Open a new Terminal and run this command to install it: sudo apt-get           install nmap.
   2. Run a scan on Kali machine by running the command: sudo nmap <vm-ip>. You can also run a scan of your host machine if you place your Kali VM on a “bridged” network.
      An Nmap scan of my host machine.
   ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/e8e12221-7d6d-411a-88f2-15d555b746c9)
   3. This scan generates several security events, such as the detection of open ports and the identification of services running on those ports. Run a few more Nmap scans          (“nmap -sS <ip address>”, “nmap -sT <ip address>”, “nmap -p- <ip address>”etc..”
   ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/ff283944-f60d-4a70-b995-0775643fc9db)

**Task 5: Querying for Security Events in the Elastic SIEM**

Now that we have forwarded data from the Kali VM to the SIEM, we can start querying and analyzing the logs in the SIEM.

To do this, follow these steps:

   1. Inside your Elastic Deployment, click on the menu icon at the top-left with the three horizontal lines and then click on the “Logs” tab under “Observability” to view          the logs from the Kali VM.
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/55db08a7-fbf0-451f-8a41-eb574ab2d020)
   2. In the search bar, enter a search query to filter the logs. For example, to search for all logs related to Nmap scans, enter the query: event.action:
      “nmap_scan” or process.args: “sudo”.
   3. Click on the “Search” button to execute the search query.
      But please note that it can sometimes take a while for the events to populate and show up on the SIEM, so this query might not work right away (I did not see results          until the next day).
   4. The results of the search query will be displayed in the table below. You can click on the three dots next to each event to view more details.

      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/945a7cae-99da-4201-bd07-fe11693e22f4)
By generating and analyzing different types of security events in Elastic SIEM like the one above, or generating authentication failures by typing in the wrong password for a user or attempting SSH logins an incorrect password, you can gain a better understanding of how security incidents are detected, investigated, and responded to in real-world environments.

**Task 6: Create a Dashboard to Visualize the Events**

You can also use the visualizations and dashboards in the SIEM app to analyze the logs and identify patterns or anomalies in the data. For example, you can create a simple dashboard that shows a count of security events over time.

Here’s how you can do that:

   1. Navigate to the Elastic web portal at <a href="https://cloud.elastic.co.">Elastic.com</a>.
   2. Click on the menu icon on the top-left, then under “Analytics,” click on “Dashboards.”
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/76771e21-2b8c-4d4b-838e-d8f3dd84d12d)
   3. Click on the “Create dashboard” button on the top right to create a new dashboard.
   4. Click on the “Create Visualization” button to add a new visualization to the dashboard.
   5. Select “Area” or “Line” as the visualization type, depending on your preference. This will create a chart that shows the count of events over time.
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/12f02603-b122-4eb3-8101-4f5e39b82ce4)
   6. In the “Metrics” section of the visualization editor on the right, select “Count” as the vertical field type and “Timestamp” for the horizontal field. This will show          the count of events over time.
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/290745e2-30b6-4c82-9ecd-3b294df3a294)
   7. Click “close” once you’re done.
   8. Click on the “Save” button to save the visualization and then complete the rest of the settings.
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/8ba2a5ea-d7f7-4a12-a2e1-420095adfaa7)
   
**Task 7: Create an Alert**

In a SIEM, alerts are a crucial feature for detecting security incidents and responding to them in a timely manner. Alerts are created based on predefined rules or custom queries, and can be configured to trigger specific actions when certain conditions are met. In this task, we will walk through the steps of creating an alert in the Elastic SIEM instance to detect Nmap scans. By following these steps, you can create an alert that will monitor your logs for Nmap scan events and then notify you when they are detected.

Here are the steps:

   1. Click on the menu icon on the top-left, then under “Security,” click on “Alerts.”
   2. Click on “Manage rules” at the top right.
    
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/1e25b6f0-8fdc-4413-b45f-f89edef66c53)
      
   5. Click on the “Create new rule” button at the top right.
   6. Under the “Define rule” section, select the “Custom query” option from the dropdown menu.
   7. Under “Custom query,” set the conditions for the rule. You can use the following query to detect Nmap scan events.
    
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/14ce5c8f-c42a-4bff-89c8-7ff4a6d28400)
      
   10. This query will match all events with the action “nmap_scan.” Then click “Continue.”
   11. Under the “About rule” section, give your rule a name and a description (Nmap Scan Detection).
   12. Set the severity level for the alert, which can help you prioritize alerts based on their importance. Keep all the other default settings under “Schedule rule” and            click “Continue.”
 
      ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/ee6cb472-c9fb-4958-83dd-38d66fd2e505)

   15. In the “Actions” section, select the action you want to take when the rule is triggered. You can choose to send an email notification, create a Slack message, or              trigger a custom webhook.
   16. Finally, click the “Create and enable rule” button to create the alert.

       ![image](https://github.com/dtntacoma/Home-Elastic-SIEM-Lab/assets/172874936/7b3028d4-2890-48b6-8af3-19565efc28fa)

Once you’ve created the alert, it will monitor your logs for Nmap scan events. If an Nmap scan event is detected, the alert will be triggered and the selected action will be taken. You can view and manage your alerts on the “Alerts” section under “Security.”

