# Croc_Pot
## INTRODUCTION :
* This project is developed for the Hak5 KeyCroc, a powerful pentesting device that should be used ethically and responsibly. Thanks to everyone at Hak5 for this platform to work on. (Croc_Pot is currently under construction and testing.)

* **Croc_Pot_Payload.txt:**
The project will start an OS detection scan to determine what OS the KeyCroc is plugged into (via USB), collect some data from the target PC, automatically start an SSH session with the connected target PC (via WiFi), and start the Croc_Pot script. Before running Croc_Pot, ensure that your KeyCroc is connected to the target PC's WiFi. If you do not have the target PC's WiFi credentials, Croc_Pot has a payload called "Croc_getonline" that will get you online (works on Windows, Raspberry Pi, and Linux).

* **Croc_Pot.sh:**
This project automates some commands for the KeyCroc for quicker setup, installation of payloads, remote connection to the KeyCroc, Nmap TCPdump target PC scan, edited files on your KeyCroc, sending emails from your KeyCroc, SSH to Hak5 gear, running Hak5 cloud C2 on the KeyCroc, checking the status of your KeyCroc, and more. 

* **TESTED ON:**
  Windows 10, Raspberry Pi 5 Bookworm, Linux Parrot OS. Sorry, no support for macOS.

## INSTALLATION :

* There are two files for this script. You will need to enter arming mode on your KeyCroc to install the files. The first file is called Croc_Pot.sh and should be placed in the **KeyCroc tools folder**. The second file is called Croc_Pot_Payload.txt and should be placed in the **KeyCroc payload folder**. Edit the Croc_Pot_Payload.txt file for your KeyCroc password (default is "hak5croc"). Ensure your KeyCroc is connected to the same local network as the target PC via WiFi.

## STARTING CROC_POT :

  - The first way to start Croc_Pot.sh is to SSH into your KeyCroc and type **/root/udisk/tools/Croc_Pot.sh**. The second way to start Croc_Pot.sh is to type **"crocpot"** anywhere, which will automatically start the Croc_Pot.sh script. It is recommended to start the Croc_Pot.sh script by typing **"crocpot"** because this payload will collect some data from the target PC. Some of the information that it will collect includes the target PC's IP address, current user name, PC host name, SSID and password, and MAC address. This information will be used in the Croc_Pot.sh script. 
  - **NOTE:** When running **crocpot**, the scan takes about 30-40 seconds to start because of OS detection, and then Croc_Pot will start.
  - **TIPS:** When Starting Croc_Pot on a new target pc
    - 1: Run **"Croc_Getonline"** payload to connect the keycroc to the target PC's WiFi.
    - 2: Run **"Croc_Unlock payload"** to get the target PC's password.
    - 3: Then type **"crocpot"** anywhere.

## SSH MENU :

 * Croc_Pot offers some SSH options that will automatically accept the SSH server's fingerprint and add it to the known hosts file. We can pass the StrictHostKeyChecking no option to SSH. For example, ssh -o "StrictHostKeyChecking no" HOST@IP.
   - **NOTE:** Automatically accepting the SSH fingerprint bypasses the security put in place by SSH, so you should be careful when using this, especially on untrusted networks such as the public internet.

 * **SSH TO HAK5 GEAR**
 * Ensure that all Hak5 gear is connected to the same local network as your Keycroc.
   - It is recommended to set up a public and private key for each of your Hak5 gear to SSH without a password.
   - To set up the SSH Keycroc to Bash Bunny connection, ensure that your Bash Bunny has an internet connection and is connected to the same PC as your Keycroc (Bash Bunny internet setup can be found at docs.hak5.org). Croc_Pot.sh will create a payload for your Bash Bunny, which will be saved on your Keycroc at tools/Croc_Pot/Bunny_Payload_Shell. Then copy this file to one of the payload switches on your Bash Bunny to start the reverse SSH tunnel to Keycroc.

### To create a public and private key:
* Perform SSH Login Without Password Using ssh-keygen & ssh-copy-id
* Step 1: Create public and private keys using ssh-key-gen on local-host
  - jsmith@local-host$ **Note: You are on local-host here**
  - jsmith@local-host$ **ssh-keygen**
  - [Press enter key]
 * Step 2: Copy the public key to remote-host using ssh-copy-id
   - jsmith@local-host$ **ssh-copy-id -i ~/.ssh/id_rsa.pub username@remote-host-ip**
   - jsmith@remote-host's password:
 * Step 3: Login to remote-host without entering the password
   - jsmith@local-host$ **ssh username@remote-host-ip**
 * The above three simple steps should get the job done in most cases.
 
 ### To set up a reverse SSH tunnel:
   - Reverse SSH is a technique that can be used to access systems (that are behind a firewall) from the outside world.
   - Here is the command for remote server side:
   - **ssh -fN -R 7000:localhost:22 username@your-Machine-ipaddress**
   - Now, do an ssh connection request from your machine to your own machine at port 7000:
   - **ssh username@localhost -p 7000**
   - Although it may seem like you are doing SSH on localhost, your request will be forwarded to the remote host. So you should use your account username on the remote server and enter the corresponding password when prompted.
   
   **SCREENSHOT**
   
![Screenshot from 2022-11-22 15-19-12](https://user-images.githubusercontent.com/71735542/203413363-a9bcc7e6-8b92-42e7-b8df-bde839439f61.png)
![Screenshot from 2022-11-22 15-25-46](https://user-images.githubusercontent.com/71735542/203414390-4a1b8808-dc07-4c9a-b781-648e7f14f2cb.png)
