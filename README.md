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

