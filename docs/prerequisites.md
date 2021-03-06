# Installing prerequisites for MountainLab

## Installing NodeJS

NodeJS is a JavaScript runtime implementation. The JavaScript programming language (not to be confused with Java) is most well known for its use in web browsers. NodeJS makes it possible to also run JavaScript on servers and desktops. MountainLab-js is implemented in JavaScript and uses NodeJS as its runtime environment.

It is important that you install a recent version of NodeJS (it is a rapidly-evolving project). It is often not sufficient to simply use the default version installed by the operating system.

For example, on Ubuntu 16.04, use the following:
```
curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
sudo apt-get install nodejs npm
```

For more information, visit [nodejs.org](https://nodejs.org).

For anaconda users, see *Using an Anaconda environment* below

## Installing MongoDB

MongoDB is a database for storing JSON documents. In contrast to structured databases built around tables, MongoDB is an example of a NoSQL key-value store. MountainLab uses MongoDB to keep track of running processor jobs, cached jobs, and SHA-1 hashes of data files.

Install MongoDB using your linux package manager. For example, on Ubuntu 16.04, use the following:

```
sudo apt-get install mongodb
```

You will then get a database daemon running on the default port of 27017. You might want to make sure this port is not exposed to the outside world (usually it wouldn't be I think).

For anaconda users, see *Using an Anaconda environment* below

## Installing Python 3 and pip

While not required for the core program, most MountainLab processor packages use Python 3.

Install Python 3 and pip using your linux package manager. For example, on Ubuntu 16.04, use the following:

```
sudo apt-get install python3 python3-pip
```

We highly recommend using a virtualenv to manage your python packages (see below).

## Using a python virtualenv

Virtual environments (virtualenv) provide a tidy way to manage python packages, without messing with the system installation. To create a new virtualenv:

```
pip3 install virtualenv
```
Note: you may need to use a different method for installing virtualenv. For example, on Ubuntu it could be that you need instead something like `sudo apt install virtualenv`.

```
cd ~
virtualenv -p python3 ml-env
```
To activate this virtualenv, use:

```
source ~/ml-env/bin/activate
```

You will notice the command-line prompt of the terminal you run the command in displays the name of this virtualenv (e.g. `(ml-env) user@host:~$`)

Now, while the virtualenv is active, any package installed using pip3 will be specific to this virtualenv (you can explore ~/ml-env to see where pip3 is placing the packages).

To deactivate, simply run:

```
deactivate
```

I personally put the above ```source ...``` line in my .bashrc file so that every time I open a terminal, I am in the default virtualenv. However, if you use pip to install packages without sudo then it installs them in `~/.local/lib/python3.6/site-packages` or similar so it is not really necessary to do this.

## Using an Anaconda environment

For users that are using a python 3.6 [Anaconda distribution](https://www.anaconda.com/distribution/), you can set up a mountainlab Anaconda environment.

Create a new python 3.6 anaconda environment:
```
conda create -n ml-env python=3.6
```
Activate this new environment:
```
source activate ml-env
```
Be sure to install any packages that you intend on using within this environment, such as ipython and jupyter:
```
conda install ipython jupyter
```

Install a current version of nodejs and mongodb from anaconda-forge
```
conda install -c conda-forge nodejs
conda install -c conda-forge mongodb
```

Install some other required packages
```
conda install -c conda-forge deepdish
conda install numpy scipy
```

For any anaconda-related problems, be sure that you are using an executable from within the environment.
