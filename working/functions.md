- clear local repo
```
git stash -u && git stash drop
```

- boot up new docker instance and enter
docker run -d -it {IMAGE_NAME}
docker container ls
docker exec -it {CONTAINER_NAME} bash

- Create image from dockerfile
```
docker build -f Dockerfile-ICCT -t icct_i .
```
-  Create container after image built
```
docker create --name icct -i icct_i
docker start icct
```
- If you're on an Apple silicone based machine you may need to execute like so
```
docker create --platform linux/amd64 --name icct -i icct_i
docker start icct

```

- Clear docker container
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```
-Clear docker images
```
docker rmi $(docker images -q)
```

## Queries:
```
docker exec -i icct gaiad version
docker exec -i icct gaiad q account cosmos1scwcfre6h4c7epkyrdfegpeaz8umqldl50gn8w --node https://rpc.cosmoshub.pupmos.network:443 -o json

osmosisd version
osmosisd q account osmo1h87gdn6wktvfmehrf2c3skpgr5872ud845ty5k --node https://rpc-osmosis-ia.notional.ventures:443 -o json

junod version
junod q account juno1taz839zt2f8pyhc6jmvrfm76ejfe0sf8jvthcy --node https://rpc.juno.pupmos.network:443 -o json

terrad version
terrad q account terra1eetusa4s0kesgug93zs8uxh0n5h6c0xvqmg0xr --node https://terra-rpc.polkachu.com:443 -o json

kujirad version
kujirad q account kujira1vsqs0d3y6ufln266r60qvszhps3tmgsxl5rmc0 --node https://kujira-rpc.polkachu.com:443 -o json
```
