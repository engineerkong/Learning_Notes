## General
- sudo -i
- sudo -s
- sudo apt-get autoclean
- pip install -e .
- conda clean --all
- conda env export > environment.yaml
- conda env create -f environment.yaml

## Docker
- sudo apt-get install docker-ce docker-ce-cli containerd.io
- sudo apt-get purge docker-ce docker-ce-cli containerd.io
- sudo cp -au /var/lib/docker /x/x/x
- sudo docker rmi image
- sudo docker build --no-cache -t demo:v1

