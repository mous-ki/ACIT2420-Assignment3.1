# ACIT2420-Assignment3.1

# Webgen Server Setup
This setup will create a system to generate and publish an HTML file with system information. THe system uses `systemd` timers to update the file daily and publish it using nginx. 

## Setup Instructions
1. **Create the `webgen` user, and directories**:
   #!/bin/bash
   sudo useradd -r -d /var/lib/webgen -s /usr/sbin/nologin webgen
   sudo mkdir -p /var/lib/webgen/{bin,HTML}
   sudo chown -R webgen:webgen /var/lib/webgen
2. Move the files to their locations:
   sudo cp files/generate_index /var/lib/webgen/bin/
   sudo chmod +x /var/lib/webgen/bin/generate_index
   sudo cp files/generate-index.service /etc/systemd/system/
   sudo cp files/generate-index.timer /etc/systemd/system/
   sudo cp files/nginx.conf /etc/nginx/nginx.conf
   sudo cp files/webgen.conf /etc/nginx/conf.d/
3. Enable and start the timer:
   sudo systemctl daemon-reload
   sudo systemctl enable --now generate-index.timer
4. Restart nginx:
   sudo systemctl restart nginx
5. Install/configure ufw:
   sudo pacman -S ufw
   sudo ufw allow ssh
   sudo ufw sllow http
   sudo ufw limit ssh
   sudo ufw enable


