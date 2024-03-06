1.	Lab - Prerequisites.

Step 1 - How to connect with the Virtual Machine.

Download the file pem_ibmcloudvsi_download.pem, the techzone page.

 <img width="425" alt="image" src="https://github.com/pecamacho/InstanaTMP/assets/86245017/2964c7c5-59ee-44e1-8721-8eef6c45df78">

Modify the permissions the file .pem
```
chmod 600 pem_ibmcloudvsi_download.pem
```

now configure the ssh connection command:

```
ssh -i pem_ibmcloudvsi_download.pem itzuser@[Public IP] -p 2223
```

Example:

ssh -i pem_ibmcloudvsi_download.pem itzuser@52.118.147.221 -p 2223

Step 2 - Installing Docker

In this lab we will use an example microservices application called Robot-Shop, it runs on Docker and as a prerequisite we need to install Docker CE

Use the command sudo to become root.
```
$ sudo -i
```
you must install Docker CE or Docker EE. Run the following commands to setup the prerequisites, download Docker CE, and install Docker CE on the virtual machine.
```
apt-get install ca-certificates curl gnupg lsb-release -y
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo   "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update -y
apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```
After the commands have executed, verify that docker is installed and running. You can run the docker ps command to confirm that it is installed and running.
```
docker ps
```
If docker is running, you should see output like what is shown below.

<img width="1073" alt="image" src="https://github.com/pecamacho/InstanaTMP/assets/86245017/814f56a3-ba35-472a-ad92-dd441c722708">

Step 3 - Installing Robot Shop

Now we are going to download the application from the repository, for that we must install git

```
apt install git
```
Now we are going to clone the repository in the virtual machine
```
cd ~ && git clone https://github.com/instana/robot-shop.git
cd robot-shop/
```
Now we must set the environment variable, "INSTANA_AGENT_KEY" with the Agent Key of the instana environment we are working on.
```
export INSTANA_AGENT_KEY=[Instana_Agent_Key]
```
Example:

export INSTANA_AGENT_KEY="thisisagentkey"
```
curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
```
docker-compose pull
```

