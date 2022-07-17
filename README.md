# Interchain Cocktail of binaries/cli tools
This is just a random assortment of Interchain binaries written so whoever wants to use them can.

## Recipe (v1)
- 1 part gaiad v7.0.2
- 1 part osmosisd v10.0.1
- 1 part junod v8.0.0
- 1 part kujirad v0.4.0

### Optional ingredients
- 1 part secretcli v1.3.1

## Notes
1. This will build up to and use 5.4GB of space on your machine once the container is built, I will attempt to optimize this
2. Dockerfile was built on ubuntu:latest with chrony added
  - This was established with a default of options 2 (America) and 85 (Los_Angeles).
  - If you would like to reconfigure it execute the following:
    - dpkg-reconfigure tzdata
  - This was then uploaded to Docker Hub under onewhiskeypls/ubuntu-chrony
  - I was not able to get debconf-set-selections to auto-input the selections, so I opted to just create an image for this
3. Obligatory verify the script contents, do not simply trust me.
- You could take this script and build a different ubuntu w/ chrony
- apt install -y chrony
4. A lot of the apt package installs were consolidated into 1 line
- See the worksheet.txt
