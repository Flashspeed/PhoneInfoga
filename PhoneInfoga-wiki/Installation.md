To install PhoneInfoga, you'll need to download source code then install dependencies.

Requirements : 

- python3 and python3-pip or Docker
- git or wget and curl

**Clone the repository :**

```shell
git clone https://github.com/sundowndev/PhoneInfoga
cd PhoneInfoga/
```

You can also download the source code archive : 

```shell
wget $(curl -s https://api.github.com/repos/sundowndev/phoneinfoga/releases/latest | grep tarball_url | cut -d '"' -f 4) -O PhoneInfoga.tar.gz
tar -xvzf PhoneInfoga.tar.gz
cd sundowndev*
```

**Install requirements :**

```shell
python3 -m pip install -r requirements.txt
```

**Create the config file :**

```shell
cp config.example.py config.py 
```

To ensure everything works, use the `-v` option to show the version : 

```shell
python3 phoneinfoga.py -v
```

### Using Docker

You can pull the repository directly from Docker hub

```shell
docker pull sundowndev/phoneinfoga:latest
```

Then run the tool

```shell
docker run --rm -it sundowndev/phoneinfoga --help
```

Or, you can download the source code, then build the docker image

#### Build

```shell
docker build --rm=true -t phoneinfoga/latest .
```

#### Usage

```shell
# docker run --rm -it phoneinfoga/latest --help
docker run --rm -it phoneinfoga/latest -n <number> [OPTIONS]
```