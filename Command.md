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
- sudo docker run -it demo bash
- sudo docker run -v <computerpath>:<containerpath> demo

# Clean up
- sudo apt-get autoclean
- conda clean --all
- pip cache purge

# SE1
- sudo docker build . -t engineerkong/se1
- sudo docker run -dt engineerkong/se1
- sudo docker exec -it xxxx bash
- phases run combo=sac_mygym ls=sac slurm=debug phases=quick task=mygym_sac num_confs=1 num_seeds=1 wandb.entity=entity_name wandb.project=project_name wandb.experiment_tag=experiment_tag
