# Humanities Research with Sound: Introduction to Audio Machine Learning

### Stephen Reid McLauglin & Tanya Clement


## Software to install before class

- Docker Community Edition or Docker Toolbox
    - [Docker CE](https://store.docker.com/search?type=edition&offering=community) (macOS/Linux)
    - [Docker Toolbox](https://www.docker.com/products/docker-toolbox) (Windows)

- Sonic Visualiser
    - [Sonic Visualiser](http://www.sonicvisualiser.org/download.html)

- Text editor: Atom or Geany
    - [https://atom.io](https://atom.io)
    - [https://www.geany.org](https://www.geany.org)


#### Up and running with Docker

First, click [here](https://github.com/hipstas/shaping-humanities-data/blob/master/audio/Fresh_Air_2017-07-31.mp3?raw=true) to download a single episode of the NPR radio show *Fresh Air*.

Open `Fresh_Air_2017-07-31.mp3` using the application `Sonic Visualiser`. When the file is open, press `g` to display a spectrogram representation of the audio.

Now open a new terminal window:

- macOS: Open the application `Terminal`, located in `/Applications/Utilities`.
- Windows: Double click `Docker Quickstart Terminal` on your desktop.
- Linux: Press `Ctrl+Alt+T` to launch a terminal window.


Now enter the following command to download the Docker image files for the Audio Labeler application. This should take several minutes.

```
docker pull hipstas/audio-labeler
```

In a new terminal window, download the Docker image files for the Audio ML Lab container.

```
docker pull hipstas/audio-ml-lab
```

Docker makes it possible to run a virtual copy of the Linux operating system within your primary OS. We will be using Ubuntu, a version of Linux that is often used to run web servers. Ordinarily, you would launch an Ubuntu server and then install the programs you need, one by one; Docker lets us speed up that process by defining our system's initial configuration in a plain text file, known as a Dockerfile. You can view the Dockerfile we are currently using [here](https://hub.docker.com/r/hipstas/audio-ml-lab/~/dockerfile/).

For a more details on how Docker works, see this [overview](https://docs.docker.com/engine/docker-overview/).

## Using Audio Labeler to generate training data

Download training dataset and launch [Audio Labeler](https://github.com/hipstas/audio-labeler) application.

```
mkdir -p ~/Desktop/audio_labeler/media/
cd ~/Desktop/audio_labeler/media/
wget http://www.stephenmclaughlin.net/HILT/audio_corpora/NPR_Fresh_Air_diarized.zip
unzip NPR_Fresh_Air_diarized.zip

docker run -it --name audio_labeler -p 8000:8000 -v ~/Desktop/audio_labeler:/home/audio_labeler hipstas/audio-labeler bash
```

Open your browser and enter `localhost:8000` in the URL bar and start labeling.



## Training and classifying.

Now enter the following command to run the Audio ML container. This will create a new directory called `sharedfolder` on your desktop.

```
docker run -d -ti --name audio_ml_lab -p 8887:8887 -v ~/Desktop/sharedfolder/:/sharedfolder/ hipstas/audio-ml-lab
docker exec -ti audio_ml_lab /bin/bash
```

The command above includes several options. The `--name` flag sets the name of our container as `audio_ml_lab`, while `-ti` tells Docker that we want to use an interactive terminal. `-p` maps port 8887 in our container to port 8887 in our local OS. `-d` puts us into detached mode, meaning we won't need to leave the terminal window open to keep Jupyter running. The `--volume` option defines a "shared volume" between the container and our local machine, a directory called `sharedfolder`. `hipstas/audio-ml-lab` identifies the container we want to download, which is hosted on the Dockerhub website.

You should now be in an interactive bash session in your new Ubuntu container. To make sure, type the following command and press enter to see your username. The response should be `root`.

```
whoami
```

Enter the following command to download the Jupyter notebook we'll be using.

```
wget https://raw.githubusercontent.com/hipstas/shaping-humanities-data/master/01_Fresh_Air_Speaker_ID.ipynb?raw=true -O 01_Fresh_Air_Speaker_ID.ipynb
```

Now open your browser and enter `localhost:8887` or `127.0.0.1:8887` in the URL bar, then click `01_Fresh_Air_Speaker_ID.ipynb` to open the notebook. We'll continue in Jupyter for the rest of this workshop.
