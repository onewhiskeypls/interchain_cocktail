clear git
```
git stash -u && git stash drop
```

boot up new docker instance and enter
sudo docker run -d -it {IMAGE_NAME}
sudo docker container ls
sudo docker exec -it {CONTAINER_NAME} bash

sudo docker create --name bins -i icct
sudo start docker bins
sudo exec -it bins bash
