# Humanities Research with Sound: Introduction to Audio Machine Learning

### Stephen Reid McLauglin & Tanya Clement

Download and launch Audio ML Lab Docker container, then launch a terminal session in the container.

```
docker rm -f audio_ml_lab
docker pull hipstas/audio-ml-lab
docker run -d -ti --name audio_ml_lab -p 8887:8887 -v ~/Desktop/sharedfolder/:/sharedfolder/ hipstas/audio-ml-lab
docker exec -ti audio_ml_lab /bin/bash
```

Download the Jupyter notebook.

```
wget https://raw.githubusercontent.com/hipstas/shaping-humanities-data/master/01_Fresh_Air_Speaker_ID.ipynb?raw=true -O 01_Fresh_Air_Speaker_ID.ipynb
```

Open your browser and enter `localhost:8887` or `127.0.0.1:8887` in the URL window, then click `01_Fresh_Air_Speaker_ID.ipynb` to open the notebook.










#Labeler UBM laptop


docker rm -f audio_labeler
docker pull hipstas/audio-labeler
docker run -it --name audio_labeler -d -p 8000:8000 -v /Volumes/U/audio_labeler:/home/audio_labeler hipstas/audio-labeler bash
