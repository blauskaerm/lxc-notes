# Init LXD

	lxd init

Add the user to the group lxd to avoid using sudo in every lxc command

# List all images

	sudo lxc image list <REMOTE>:

This lists all available images

# Filter images

	sudo lxc image list <REMOTE>:kali

This shows all images associated to Kali

# List remote servers contaning images

There are by default tree remote servers with images and are shown with the
remote command

	sudo lxc remote list

# Create/launch LXC container

Images are identified using either image alias or fingerprint.
To launch a container using alias

	sudo lxc launch <REMOTE>:<IMAGE ALIAS> <CONTAINER NAME> -c security.privileged=true

Similarly using fingerprint

	sudo lxc launch <REMOTE>:<FINGERPRINT> <CONTAINER NAME> -c security.privileged=true

This starts the containers in privilaged mode and is not recommended by the
Arch wiki.

# Snapshot

## Create a snapshot

	sudo lxc snapshot <CONTAINER NAME> <SNAPSHOT NAME>

## Get container name and available snapshots

This command also lists all information about the container. The amount of
snapshots for each container can also be seen as a metric with lxc list.

	sudo lxc info <CONTAINER NAME>

## Restore from snapshot

	sudo lxc restore <CONTAINER NAME> <SNAPSHOT NAME>

## Delete snapshot

	sudo lxc delete <CONTAINER NAME>/<SNAPSHOT NAME>

# Limit amount of memory

	sudo lxc config set <CONTAINER NAME> limits.memory 256MB

# Port forward

Forward host TCP port 80 to container port 80.
Port name is an administrative name and can be anything.

	sudo lxc config device add <CONTAINER NAME> <PORT NAME> proxy listen=tcp:0.0.0.0:80 connect=tcp:127.0.0.1:80

# Logging in using sudo

This is a trick to login as a user using sudo

	sudo lxc exec <CONTAINER NAME> -- sudo --user <USERNAME> --login

# Good to know commands

Disable container autostart

	sudo lxc config set <CONTAINER NAME> boot.autostart false

Mount a directory

	lxc config device add <CONTAINER NAME> <MOUNT NAME> disk source=<HOST SOURCE> path=<CONTAINER DESTINATION>

# Notes

Its recommended to run all containers in unprivileged mode.
This is not set up by default in Manjaro.

# Links

  * https://wiki.archlinux.org/index.php/LXD#Launching_container_without_CONFIG_USER_NS
  * https://wiki.archlinux.org/index.php/Linux_Containers#Enable_support_to_run_unprivileged_containers_(optional)
