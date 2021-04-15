# Installing VNC on Raspberry Pi 3B+ with Ubuntu 20.10 32bit
This was done so that the enablement of RealVNC on Raspberry PI 3 B+ running
Ubuntu Groovy Gorilla (20.10) 32bit could work

Found this on: https://www.raspberrypi.org/forums/viewtopic.php?t=288769[](https://www.raspberrypi.org/forums/viewtopic.php?t=288769)

The folks that inspired me to write this bash script to help others are 
soma72 for the original instructions, pucasso, kazin08 and Ghost_Rider51 for cracking the code
With their instructions below 

## The steps documented to work
By pucasso, kazin08 and Ghost_Rider51

	# Download package required
	# source: http://archive.raspberrypi.org/debian/pool/main/r/realvnc-vnc/
	wget https://archive.raspberrypi.org/debian/pool/main/r/realvnc-vnc/realvnc-vnc-server_6.7.2.42622_armhf.deb
	
	# Install package
	sudo dpkg -i realvnc-vnc-server_6.7.2.42622_armhf.deb

	# Change over to the arm-linux-gnueabihf folder under /usr/lib
	cd /usr/lib/arm-linux-gnueabihf

	# As sudo create symlinks to the following files
	sudo ln libvcos.so /usr/lib/libvcos.so.0
	sudo ln libvchiq_arm.so /usr/lib/libvchiq_arm.so.0
	sudo ln libbcm_host.so /usr/lib/libbcm_host.so.0
	#libbcm_host.so
	# libvcos.so
	sudo ln libmmal.so
	sudo ln libmmal_core.so
	sudo ln libmmal_components.so
	sudo ln libmmal_util.so
	sudo ln libmmal_vc_client.so
	sudo ln libvcsm.so
	sudo ln libcontainers.so

	sudo systemctl enable vncserver-virtuald.service
	sudo systemctl enable vncserver-x11-serviced.service
	sudo systemctl start vncserver-virtuald.service
	sudo systemctl start vncserver-x11-serviced.service
	# sudo reboot
	
# Script to autoinstall
This will be helpful when having to do this across several RPis.
BASH Script based on those documented steps.

[install-real-vnc-server-rpi3-ubuntu20.04.sh](install-real-vnc-server-rpi3-ubuntu20.04.sh)

To run it you must run as sudo 

    # chmod the script first
    chmod +x install-real-vnc-server-rpi3-ubuntu20.04.sh
    
    sudo ./install-real-vnc-server-rpi3-ubuntu20.04.sh
    
**E.g.**

    You are about to install RealVNC Server for Raspberry Pi 3
    realvnc-vnc-server_6.7.2.42622_armhf.deb
    Running OS Ubuntu 20.10 32bit
    
    
    Would you like to continue?
    Enter 'y' for yes or 'n' for No :
    y
    
    Installing VNC Server : realvnc-vnc-server_6.7.2.42622_armhf.deb...
    
    attempting to create symlink file /usr/lib/libvchiq_arm.so.0...
    attempting to create symlink file /usr/lib/libbcm_host.so.0...
    attempting to create symlink file /usr/lib/libvcos.so.0...
    attempting to create symlink file /usr/lib/libmmal.so.0...
    attempting to create symlink file /usr/lib/libmmal_core.so.0...
    attempting to create symlink file /usr/lib/libmmal_components.so.0...
    attempting to create symlink file /usr/lib/libmmal_util.so.0...
    attempting to create symlink file /usr/lib/libmmal_vc_client.so.0...
    attempting to create symlink file /usr/lib/libchiq_arm.so.0...
    attempting to create symlink file /usr/lib/libvcsm.so.0...
    attempting to create symlink file /usr/lib/libcontainers.so.0...

    Enabling and starting the service vncserver-virtuald.service...
    Enabling and starting the service vncserver-x11-serviced.service...
    RealVNC Server : realvnc-vnc-server_6.7.2.42622_armhf.deb has been installed.

    System needs to be rebooted.
    Would you like to reboot it now?
    Enter 'y' for yes or 'n' for No :
    n
    # No was selected
    No worries you can always reboot when you are ready.
    You can reboot with the command
    'sudo shutdown -r now'
    
That is pretty much it. Please feel free to modify the logic in script to
make it better.
    
    

    

    


