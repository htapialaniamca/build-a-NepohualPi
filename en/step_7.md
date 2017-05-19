# Set up the client on the OctaPi network

1. Connect a monitor, keyboard and mouse and power up a Raspberry Pi containing the **client** SD card you created earlier.

1. Repeat the instructions from the previous step but this time on the **client**, logging onto the "OctaPi" network and removing any alternative Wi-Fi details from `wpa_suplicant`.

1. Keeping the client switched on, boot up the single **server** Raspberry Pi with only a power lead connected.

1. Open a terminal window on the **client** Raspberry Pi and type the following command to find out the IP address of the **server** Raspberry Pi:

    ```bash
    nmap -sP 192.168.1.*
    ```

    Make a note of the **server** IP address (you should see the router's address and the client's address listed too)

    **IMPORTANT:** The `nmap` software scans the network to find the IP addresses of the devices connected to it. We need to do this on our local network (LAN) so that the client machine can communicate with the Raspberry Pi computers which form the OctaPi cluster. **Do not run nmap on a network that is connected to the internet.** nmap is a powerful piece of software and using it to scan a network you do not own may be considered 'hacking', and in some countries may even be illegal.

1. On the **client**, run `ssh-keygen` in the terminal to create a key for authenticating the client with the server.

    ```bash
    ssh-keygen;
    ```

    This key is used to help the `cluster_action.sh` script (provided with the client software) to run with the servers.

1. Find the IP address of the server machine you noted down earlier, and replacing `<remote ip>` with the **server's** IP address, run this command in a terminal to copy the key to the server:

    ```bash
    ssh-copy-id -i ~/.ssh/id_rsa.pub <remote ip>
    ```

    This completes preparation of the client and server, we now need to check everything is correct and working properly with a single server.