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

Open a new terminal window:

- macOS: Open the application `Terminal`, located in `/Applications/Utilities`.
- Windows: Double click `Docker Quickstart Terminal` on your desktop.
- Linux: Press `Ctrl+Alt+T` to launch a terminal window.

Now enter the following command to download the image files we'll be using. This should take several minutes.

```
docker pull hipstas/audio-ml-lab
```

Docker makes it possible to run a virtual copy of the Linux operating system within your primary OS. We will be using Ubuntu, a version of Linux that is often used to run web servers. Ordinarily, you would launch an Ubuntu server and then install the programs you need, one by one; Docker lets us speed up that process by defining our system's initial configuration in a plain text file, known as a Dockerfile. You can view the Dockerfile we are currently using [here](https://hub.docker.com/r/hipstas/audio-ml-lab/~/dockerfile/).

For a more details on how Docker works, see this [overview](https://docs.docker.com/engine/docker-overview/).

When the download is complete, enter the following command to run the container. This will create a new directory called `sharedfolder` on your desktop.

Enter the following commands to launch the Audio ML Lab Docker container, then launch a terminal session in the container.

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

Now open your browser and enter `localhost:8887` or `127.0.0.1:8887` in the URL window, then click `01_Fresh_Air_Speaker_ID.ipynb` to open the notebook.
