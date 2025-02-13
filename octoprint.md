## Octoprint

### Install Octoprint on linux distro

> Installing OctoPrint should be done within a virtual environment, rather than an OS wide install, to help prevent dependency conflicts. To setup Python, dependencies and the virtual environment, run

```
cd ~
sudo apt update
sudo apt install python3 python3-pip python3-dev python3-setuptools python3-venv git libyaml-dev build-essential libffi-dev libssl-dev
mkdir OctoPrint && cd OctoPrint
python3 -m venv venv
source venv/bin/activate
```

In virtual enviroment install:

```
pip install --upgrade pip wheel
pip install octoprint
```

To run again Octoprint need to be in OctoPrint folder (likly to be in home folder) and run:

```
python3 -m venv venv
source venv/bin/activate 
```

---
