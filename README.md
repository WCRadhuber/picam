# Picam
> Designed for a raspberry pi running PI OS

Picam is a video streaming API and web app using Picamera.


# Ansible Installation
Can be installed using the provided picam_install.yml file with ansible. Be sure to have the camera connected properly on host machine. Ansible must be installed and configured appropriately on your administration machine for this method.

```bash
git clone https://github.com/WCRadhuber/picam.git

ansible-playbook --ask-become-pass ./picam/picam_install.yml -- limit YOUR_HOSTS

rm -rf ./picam
```

# Manuall Installation
To install manually, run the following commands. This will create the service under the installation user, if you'd like to change what user the service runs as be sure to update the $USER value in the provided commands. This will also leave picam_install.yml in /opt/ which can be removed or used for later installations.

```bash
git clone https://github.com/WCRadhuber/picam.git

sed -i "s/YOUR_USER/$USER" ./picam/picam.service

sudo mv -p ./picam /opt/picam

sudo mv /opt/picam/picam.sh /usr/local/bin/picam.sh

sudo mv /opt/picam/picam.service /etc/systemd/system/picam.service

sudo systemctl daemon-reload

sudo systemctl enable --now picam.service
```

# After Installation
Enter your machines ip address at port 8000 into the browser. This will redirect you to the index.html page. The api can stream can be captured at ip-addr:8000/stream.mjpg
