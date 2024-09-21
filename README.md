Splunk Homelab: Setting Up and Configuring Splunk for Security Monitoring


* Part 1:
    * Creating the Ubuntu VM
        * -> Create a New VM: Use Virtual Box
        * -> Configure VM Settings:Memory 4gb (RAM) and Hard disk 100 GB
    * Network Configuration:Change Network Interface for the VM to LAN 4
    * Installing Ubuntu
        * Install VirtualBox Guest Additions
    * Create a Snapshot : Fresh Ubuntu Installed
    * We need splunk for Ubuntu : Installing Splunk on Ubuntu
        * Install Dependencies Dependencies and repos for Splunk in Ubuntu
        * Install Splunk:
        * Dpkg splunk Debian file
        * Accept Splunk License through /opt/splunk/bin
        * Enable Splunk to Start at Boot:
    * Create a Snapshot: Ubuntu Snapshot after installing splunk on Ubuntu Machine

* Part 2: 
    * Configuring Splunk for Data Ingestion
        * Setting Up Splunk to Receive Data
            * Visit : http://localhost:8000/ or visit http://127.0.0.1:8000/ which ever comfortable
            * Now configure the forwarder in splunk console:
                * Settings > Forwarding and Receiving.
                * ->Under “Receive data,” I clicked “Add new” and set the listening port to 9997 (Note: Defaults are 9997 for forwarders to the Splunk indexer)
            * Now we need Windows Server as Domain Controller to ingest or forward data to Splunk Ubuntu Instance
                * We need Configuring Splunk Universal Forwarder on Windows Server 2019
                * Download Universal Forwarder:> From Splunk Site
                * Install the Forwarder: In the newly installed DC controller ie: Windows Server (Note we need forest and domain created for Windows server to act as DC controller to assign IPs to different VMs) ie set static ip for Ubuntu through Network Interface settings in Virtual Box for Ubuntu
            * After installation : We need to configure DC controller through port 8089 ie Splunk Deployment server ie plunked
                * Points:
                    * Host Configuration : IP of Windows DC machine: Check IPconfig or through server manager to find ip of Windows Server set IP and Port to 8089
                    * Receiver Configuration: Receiver Indexer : IP of Ubuntu and port should be 9997 as tcp/udp as we forward data to Ubuntu Splunk Machine
* Part 3: 
    * Configuring Data Ingestion
        * Add Data Source in Splunk
            * Go to splunk console through localhost:8000 > Settings > Add Data> Forward
            * Now we add Windows server DC controller so we get all logs and event logs from Windows Server to our splunk instance
            * Give a name WindowsLogs for storing those ingested logs.
            * Verify Data Ingestion: Click on Searching and Reporting from Dashboard
        * Search any query : index=“*” (* is a wild card here) index will show all data

* Splunk is configured for only forwarding Windows Server Machine .
    * Create some VM with outdated windows and assign IP and username and password through DC controller and connect to domain and use the VM as sandbox to infect as all pc connected to DC domain will forward logs to splunk
