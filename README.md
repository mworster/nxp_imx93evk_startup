# nxp_imx93evk_startup
Notes on getting the i.mx93 EVK running and updated on a new system

This is how to get up and running doing new builds for the i.MX93evk:
https://www.nxp.com/design/design-center/development-boards-and-designs/i-mx-evaluation-and-development-boards/i-mx-93-evaluation-kit:i.MX93EVK

First we're going to download a Linux platform to work on. I have had issues using the integrated WSL in the past so instead we're going to use Oracle Virtual box. 

Start by downloading Virtual box from The site:
https://www.virtualbox.org/wiki/Download_Old_Builds_7_0

Note in this instance we're picking an older 7.0 version since the latest (7.0.16) has a warning on it that it crashes. 

For the iso to install I picked Ubuntu 22.04
https://www.releases.ubuntu.com/22.04/

The latest at this time (24.04) wouldn't load in the virtual box, and that's fine, we don't need the latest and greatest at this time.

After picking 20 cores and 25GB of RAM it was time to launch the VM and install Ubuntu.

You'll want to enable the bidirectioal clipboard under devices->shared clipboard

With the VM up and running we can follow the Yocto User's guide from NXP to get the basics installed:
https://www.nxp.com/docs/en/user-guide/IMX_YOCTO_PROJECT_USERS_GUIDE.pdf

First the guide says that we need to install the compents in a seperate guide:
https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html#yocto-project-quick-build

$ sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev python3-subunit mesa-common-dev zstd liblz4-tool file locales libacl1
$ sudo locale-gen en_US.UTF-8

Since this is a fresh machine you'll also need to install curl:

$ sudo apt install curl

Once you have curl then you can download repo:

$ mkdir ~/bin (this step may not be needed if the bin folder already exists)
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo

and set that to your path:
export PATH=~/bin:$PATH

Then setup git:
$ git config --global user.name "Your Name"
$ git config --global user.email "Your Email"
$ git config --global color.ui auto

Then setup the repo

$ mkdir imx-yocto-bsp
$ cd imx-yocto-bsp
$ repo init -u https://github.com/nxp-imx/imx-manifest
-b imx-linux-kirkstone -m imx-5.15.52-2.1.0.xml
$ repo sync


Finally it's time to run the setup script and do the build. 
$ DISTRO=fsl-imx-wayland MACHINE=imx93evk source imx-setup-release.sh -b
 build_dir

 This sets up the wayland UI backend and our target machine and drops us in the newly created `build_dir` directory. 

Now attempt to build the target:

$ builddir > bitbake imx-image-core
