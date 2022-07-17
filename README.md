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
1. This will build up to and use 5.4GB of space on your machine once the container is built, I will attempt to optimize this.
    - Update: I failed
2. Dockerfile was built on ubuntu:latest with chrony added
    - This was established with a default of options 2 (America) and 85 (Los_Angeles).
    - If you would like to reconfigure it execute the following:
        - `dpkg-reconfigure tzdata`
    - This was then uploaded to Docker Hub under onewhiskeypls/ubuntu-chrony
    - I was not able to get debconf-set-selections to auto-input the selections, so I opted to just create an image for this
3. Obligatory verify the script contents, do not simply trust me.
    - You could take this script and build a different ubuntu w/ chrony
    - `apt install -y chrony`
4. A lot of the apt package installs were consolidated into 1 line
    - See the worksheet.txt

## Resources
|Chain|Bin|Version|RPC|
|-|-|-|--|
|Cosmos Hub|gaiad|v7.0.2| https://rpc.cosmoshub.pupmos.network:443 |
|Osmosis|osmosisd|v10.0.1| https://rpc-osmosis-ia.notional.ventures:443 |
|Juno|junod|v8.0.0| https://rpc.juno.pupmos.network:443 |
|Terra2|terrad|v2.0.1| https://terra-rpc.polkachu.com:443 |
|Kujira|kujirad|v0.4.0| https://kujira-rpc.polkachu.com:443 |
|Secret*|secretcli|v1.3.1| https://scrt-rpc.blockpane.com:443 |

- you will need to manually install Secret. See instructions below

MISC Resources:
- https://cosmos.directory/
  - You can find other RPCs and info here

## How to run
Notes
1. You will need Docker on your machine
    - https://docs.docker.com/engine/install/
    - https://docs.docker.com/get-docker/
2. You will need git installed OR find your way to cloning this repo
    - https://git-scm.com/book/en/v2/Getting-Started-Installing-Git

- Create the image
Note: *You may need `sudo` in front of these commands depending on your account's permissions*

```
docker build -f Dockerfile-ICCT . -t icct_i
```

- This will create the container, start it then push you in to the container in interactive mode
```
sudo docker create -i icct_i --name icct
sudo start docker icct
sudo exec -it icct bash
```

- Optional while in the cli
You may execute the following to ensure it's working properly
```
gaiad version
gaiad q account cosmos1scwcfre6h4c7epkyrdfegpeaz8umqldl50gn8w --node https://rpc.cosmoshub.pupmos.network:443 -o json

osmosisd version
osmosisd q account osmo1h87gdn6wktvfmehrf2c3skpgr5872ud845ty5k --node https://rpc-osmosis-ia.notional.ventures:443 -o json

junod version
junod q account juno1taz839zt2f8pyhc6jmvrfm76ejfe0sf8jvthcy --node https://rpc.juno.pupmos.network:443 -o json

terrad version
terrad q account terra1eetusa4s0kesgug93zs8uxh0n5h6c0xvqmg0xr --node https://terra-rpc.polkachu.com:443 -o json

kujirad version
kujirad q account kujira1vsqs0d3y6ufln266r60qvszhps3tmgsxl5rmc0 --node https://kujira-rpc.polkachu.com:443 -o json

#secretcli version
#secretcli q account secret1dn540qzhd3kuml0t09zr575yam74tzhqtdf7se --node https://scrt-rpc.blockpane.com:443 -o json
```

### Optional - Installing secretcli
Note: I had a few troubles with this one, so don't be surprised if this barfs. This was likely due to needing to install the SGX.  It threw errors often when building other packages, so I wasn't comfortable allowing it to automate
```
# "INSTALL secretcli"
# "zombied from https://docs.scrt.network/docs/node-runners/node-setup/install-secretd"

cd ~/dev
wget "https://github.com/scrtlabs/SecretNetwork/releases/download/v1.3.1/secretnetwork_1.3.1_mainnet_rocksdb_amd64.deb"
apt install -y libsnappy1v5
dpkg -i secretnetwork_1.3.1_mainnet_rocksdb_amd64.deb
rm secretnetwork_1.3.1_mainnet_rocksdb_amd64.deb
secretcli q account secret1dn540qzhd3kuml0t09zr575yam74tzhqtdf7se --node https://scrt-rpc.blockpane.com:443 -o json
```
