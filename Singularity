################################################################################
# Basic bootstrap definition to build CentOS 7 container from Docker container
################################################################################

BootStrap: docker
From: jasongallant/singular_shockly

################################################################################
# Copy any necessary files into the container
################################################################################
#%files
#~/my_file /path/in/container

%post
################################################################################
# Install additional login shells for users that need them
################################################################################
#yum -y install tcsh ksh zsh

################################################################################
# Install additional packages
################################################################################

################################################################################
# Create directories to enable access to common HPCC mount points
################################################################################
mkdir -p /home
mkdir -p /mnt/scratch

################################################################################
# Run the user's login shell, or a user specified command
################################################################################
%runscript
SHELL="$(getent passwd $USER | awk -F: '{print $NF}')"
SHELL=${SHELL:-/bin/bash}
if [[ "$@" == "" ]]; then
  exec env -i TERM="$TERM" HOME="$HOME" $SHELL -l
else
  exec env -i TERM="$TERM" HOME="$HOME" $@
fi
