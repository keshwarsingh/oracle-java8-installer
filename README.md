# oracle-java8-installer
Oracle Java 8 packages for Ubuntu - The Oracle JDK License has changed for releases starting April 16, 2019.
Please note that Java 8 reached its end of public updates and Oracle will not release any more updates after January 2019. For details please see https://www.oracle.com/technetwork/java/java-se-support-roadmap.html

Introduction
------------

Oracle Java 8 packages for Ubuntu

Supported Ubuntu version
-------------------------

So far packages were tested on following Ubuntu version:

- bionic amd64
- focal amd64

Usage
-----

To build the packages:

- Save the script as `install_java8.sh`
- Make it executable: `chmod +x install_java8.sh`
- Run the script: `./install_java8.sh`

    #!/bin/bash
    
    # Exit immediately if a command exits with a non-zero status
    set -e
    
    # Install required packages
    echo "Installing required packages..."
    sudo apt update
    sudo apt install -y build-essential debhelper java-common git
    
    # Clone the repository
    echo "Cloning the Oracle Java 8 Installer repository..."
    git clone https://github.com/keshwarsingh/oracle-java8-installer.git
    cd oracle-java8-installer
    
    # Prompt user to download necessary files
    echo "Please download the following files and place them in the current directory:"
    echo "1. JDK: https://www.oracle.com/java/technologies/downloads/"
    echo "2. JCE: https://www.oracle.com/java/technologies/javase-jce8-downloads.html"
    echo "Press Enter when you have downloaded the files."
    read -r
    
    # Build the package
    echo "Building the Debian packages..."
    dpkg-buildpackage -uc -us || {
        echo "dpkg-buildpackage failed. Installing missing dependencies..."
        sudo apt-get install -f
        dpkg-buildpackage -uc -us
    }
    
    # Install the built packages
    echo "Installing the built packages..."
    sudo apt-get install ../oracle-java8-installer_8.431.1_amd64.deb \
                         ../oracle-java8-unlimited-jce-policy_8.431.1_all.deb \
                         ../oracle-java8-set-default_8.431.1_all.deb
    
    echo "Installation complete!"
