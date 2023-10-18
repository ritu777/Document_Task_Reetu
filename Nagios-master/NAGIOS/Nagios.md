
  
<u><h1 style="text-align:center">Installation of Nagios in Ubuntu 20.04 </h1></u>

<u><h2>Task requirement</h2></u></br>

To track the status and performance of their IT infrastructure. It provides a centralized platform for monitoring hosts, services, and network devices, 

<u><h2 >Environment details </h2></u>
**Os**- Ubuntu 20.04</br>
**Cpu**- 8 Core</br>
**Storage**- 1 TB</br>

<u><h2 >Tool used </h2></u>

- podman version (3.4.2)
- Nagios version (4.4.8)
  
<u><h3 >Here are some steps for installing nagios in container: </h3></u>

##### Command 1:-
This command is used for installation of podman.
```
apt install -y podman
```
**apt:** apt stands for "Advanced Package Tool. It is used to install, update, and manage software packages on the system.</br>

**install:** This is the sub-command that tells apt to install a package. When you use apt install, you're instructing the package manager to download and install the specified software.</br>

**-y:** This is an option flag that stands for "yes." It's used to automatically answer "yes" to any prompts that may come up during the installation process.</br>        

**podman:** This is the name of the package or software you want to install.

##### Command 2:-
This command will query the default container registry (usually Docker Hub) and return a list of container images with "nagios" in their name or description.
```
podman search nagios
```
![Alt text](image-fotor-20230909690.png)

**podman:** It is the name of the containerization tool.</br>

**search:** It is a subcommand in a podman tool, it indicates that you want to search for container image images in container registry.</br>

**nagios:** It is search term or query, here I am  looking for container images related to the Nagios monitoring tool.</br>

##### Command 3:-
This comand is used to pull the nagios container image from docker hub to your local system using podman.
```
podman pull docker.io/jasonrivers/nagios  
```
![Alt text](<Screenshot from 2023-09-04 20-07-24-fotor-2023090962043.png>)

**podman pull:** It tells your computer to download something.</br>

**docker.io:** It's the location on the internet where we want to get something.</br>

**jasonrivers/nagios:** This specifies exactly what we want to download, in this case, it's a tool or application called "nagios."</br>



##### Command 4:- 
This command will start the Nagios container with the specified options. You can access the Nagios web interface by opening a web browser and navigating to http://localhost:8095/nagios.</br> 
In this command I added my username and password also otherwise nagios will give you default username and password.

```
 podman run -d --name nagios -p 8095:80 --cap-add=NET_RAW -e NAGIOSADMIN_USER=reetu -e NAGIOSADMIN_PASSWORD=nagios docker.io/jasonrivers/nagios
 ```
![Alt text](run-fotor-2023090963145-fotor-2023090911117.png)

**podman run:** It tells your computer to start running something in a container.</br>

**-d:** It stands for "detached mode." This means that the container will run in the background, and you'll get your command prompt back.</br>

**--name nagios:** This gives your container a name, in this case, "nagios." It's like giving it a label so you can refer to it easily.</br>

**-p 8095:80:** This maps port 8095 on your computer to port 80 in the container. So, when you access port 8095 on your computer, it's like talking to port 80 in the container.</br>

**--cap-add=NET_RAW:** This adds the capability to send and receive raw network packets. It's needed for certain network-related tasks.

**-e NAGIOSADMIN_USER=reetu:** This sets an environment variable NAGIOSADMIN_USER inside the container to "reetu." It's like giving a piece of information to the container.</br>

**-e NAGIOSADMIN_PASSWORD=nagios:** This sets another environment variable NAGIOSADMIN_PASSWORD inside the container to "nagios." It's like giving another piece of information to the container.</br>

**docker.io/jasonrivers/nagios:** This is the name of the container image you want to run. It's like specifying which application or tool you want to use in the container.</br>

##### Command 5 :-
 Check running container details by this command.
 ```
podman ps
```
![Alt text](<podman ps-fotor-20230909105549.png>)
**podman:** This is the command-line tool for managing containers.</br>

**ps:** This is a subcommand of podman that stands for "processes" or "list containers."</br>

##### Command 6:-
This command is used for going into the container and execute commands.
```
podman exec -it nagios bash
```
![Alt text](<Screenshot from 2023-09-09 11-03-36-fotor-202309091163.png>)

**podman exec:** Exec is the sub command of podman used for executing a command inside a running container.</br>

**-it:** It allows you to run interactive commands inside containers while maintaining a terminal-like environment for a smooth interactive experience.</br>

**nagios:** This is the name of the container where you want to execute the command. It specifies which container to enter.</br>

**bash:** This is the command you want to run inside the container. In this case, you are starting a Bash shell inside the container. Bash is a command-line shell that allows you to interact with the container's file system and execute commands within it.

##### Command 7:-
By this command, I am telling my computer to change my current working directory to the /opt/nagios/etc directory.

```
cd /opt/nagios/etc
```
**cd:** This is a command that stands for "change directory." It is used to navigate or move to a different directory (folder) in the file system.

**/opt/nagios/etc:** This is the path or location you want to change your current directory to. In this case, you are specifying the directory /opt/nagios/etc as the target directory.

![Alt text](<Screenshot from 2023-09-09 11-08-52-fotor-20230909111153.png>)

##### Command 8:-
```
ls
```
![Alt text](<Screenshot from 2023-09-09 11-13-39-fotor-20230909113319.png>)


##### Command 9:-
This command is used  for editing in file.

```
vim cgi.cfg
```

Go to the cgi.cfg file and add your username which you have mentioned in run command.</BR>
![Alt text](<Screenshot from 2023-09-09 11-53-29-fotor-20230909115510-fotor-2023090912821.png>)

**vim:** This is the name of a text editor program.

**cgi.cfg:**  This appears to be a filename or file path.


Type **localhost:8095** on web page and then you have to login by username and password.</br>


![Alt text](login.png)

After login you will get Nagios dashboard like this:

![Alt text](<Screenshot from 2023-09-08 11-34-20.png>) 

#### Checking services
We have to go on left side and click on the service option.
This is the dashboard of all services.</br>





 

![Alt text](<Screenshot from 2023-09-08 23-30-45.png>)
