## General
- sudo -i
- sudo -s
- pip install -e . (dev 本库链接 install 另建库在env中)
- conda env export > environment.yaml
- conda env create -f environment.yaml

## Docker
- sudo apt-get install docker-ce docker-ce-cli containerd.io
- sudo apt-get purge docker-ce docker-ce-cli containerd.io
- sudo cp -au /var/lib/docker /x/x/x
- sudo docker rmi image
- sudo docker system prune -a
- sudo docker build --no-cache -t demo:v1 .

# Clean up
- sudo apt-get autoclean
- conda clean --all
- pip cache purge
