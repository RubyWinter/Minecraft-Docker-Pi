# Minecraft-Docker-Pi
Installation of a Minecraft Java Server on a Raspberry Pi using Docker.

Please ensure that you have a raspberry pi 4 with raspberry pi lite OS installed with SSH
enabled as well as Docker set up on it.

If you haven't yet, install java with this command
sudo apt install default-jdk

Minecraft Docker (after docker is set up)

Follow the first commands in the document I have provided up until copying the first body
of text into the new document you created.
After setting up the initial document, close it by hitting "ctrl-x", then "y", then "enter"
Change to Home directory using: ~cd
Download ngrok using the next command:
wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-arm.tgz
tar -xvzf ngrok-stable-linux-arm.tgz

Extract the file you just downloaded and configure your token using the next 2 commands
listed in the document I provided.

open the file with nano
sudo nano /home/pi/.ngrok2/ngrok.yml

Followed by copying and pasting this:
tunnels:
  minecraft-server:
    proto: tcp
    addr: 25565
    bind-tls: true
    console_ui: false

//enable ngrok as a service
sudo nano /etc/systemd/system/ngrok-client.service

//paste the following
[Unit]
Description=ngrok client
After=network.target

[Service]
ExecStart=/home/pi/ngrok start --all -config /home/pi/.ngrok2/ngrok.yml
Restart=on-abort

[Install]
WantedBy=multi-user.target

//then run these commands
sudo systemctl daemon-reload
sudo systemctl enable ngrok-client
sudo systemctl start ngrok-client
