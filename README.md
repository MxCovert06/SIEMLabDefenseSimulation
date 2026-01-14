# SIEMLabDefenseSimulation

This is a project I took interest in because of the current path I am following in HackTheBox and TryHackMe.
I have always taken an interest in catching attacks as they happen, yet also being able to simulate attacks is equally as important. This lab aims to hold both ends of this interest as I can launch attacks onto an enterprise infrastructure simulation, and be able to see what an SOC analyst would see as it happened.

# Learning Objectives
I expect to learn from this project a variety of technologies I have never self-hosted before. This will be my first time using Docker as well as Docker Compose (To host a multi-part infrastructure). I have also never self hosted my own SIEM purple-team lab, so this should be a great way to learn installation, utilization, and challenges present.

# How I Modeled The Infrastructure:

I made a simple, yet telling model for this infrastructure. Using the POP_OS as the intermediary in between the Attacker and Target simulates an internal server being probed by an external machine. Oftentimes, in smaller businesses there is not much budget for DMZ's or enhanced security solutions, so utilizing a single server that forwards requests is a normality.

<img width="1695" height="718" alt="Blank diagram" src="https://github.com/user-attachments/assets/4e8e466f-da29-4a50-9b5a-521eceebf02f" />

Working with VirtualBox to tune the settings of each Virtual machine required some tinkering, however, initial contact was possible between all three machines. I was able to get each machine to ping each other reliably. Using the "bridged" adapter helped immensly, and allowed contact between the three.

<img width="3148" height="797" alt="Blank diagram (1)" src="https://github.com/user-attachments/assets/9ac6dac5-7ae5-419f-a14c-c94086d4a439" />

# Installation of Elastic

To get my lab set up, I had Kali Linux, A Windows 10 VM with the FLARE VM suite of tools installed (The only tool we will use is SysMon and ProcMon), and POP_OS which will have elastic installed.
I will utilize docker to host the Elasticsearch and Kibana. Let us proceed with the installation of Docker

# Docker installation
`sudo apt install docker.io` - Installed Docker for me

After searching how to install Elastic and its counterparts through Docker, I made it to the pull sections for each version. These versions run on specific CPU architectures. To check our specific architecture, I used `uname -m` and it showed `x86_64`. I will use version `elasticsearch:9.2.4-amd64` for this lab and its corresponding Kibana version. Elastic makes it easy to install direct by supplying the Docker command needed to install the stack.

I used the documentation present on Elastic's official site to install, following each instruction. Having both of my docker 
containers present, I wrote a shell script to automatically start my containers without typing in a long command each time
