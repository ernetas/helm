# Helm Debian/Ubuntu package

While Helm is a fairly mature project, it still doesn't have Debian/Ubuntu packages outside official Debian/Ubuntu repositories, which are often out of date. This aims at providing DEB packaging for that great project.

Currently, we're building packages only for Ubuntu 16.04 and 18.04, but they have been tested and known to work on other Debian and Ubuntu versions.

## Building packages
You can build packages yourself by running `make`. Requirements: `make` (obviously), `docker`, `sed`, `wget`. This will generate a `helm-*.deb` file locally.

Building packages modifies some files in `package` directory, so please do not commit them - instead, commit your changes before building and reset after building.

## Using apt repository
These packages are published on apt.trys.eu. To use that repo, you first need to trust my gpg key:

```
apt-key adv --keyserver keyserver.ubuntu.com --recv B2902044AD3A8C3552B419C43616C413CFA7D784
```

Then install `apt-transport-https`:

```
apt-get update
apt-get install -y apt-transport-https
```

Finally create `/etc/apt/sources.list.d/apt-trys-eu.list` with contents `deb https://apt.trys.eu/ /` and run `apt-get update`:

```
echo 'deb https://apt.trys.eu/ /' | sudo tee /etc/apt/sources.list.d/apt-trys-eu.list 
apt-get update
```

Testing: `apt-cache policy helm | grep apt.trys.eu | head -n1` should show:

```
       500 https://apt.trys.eu  Packages
```

Note that this is not a dedicated repository for Docker Compose, nor an official one. I am in no way affiliated with Docker, just a poor man trying to make my life easier deploying and managing Docker Compose versions across hundreds or machines owned by separate entities. I recommend to use apt pinning to make sure that packages from this repo do not override packages from your system, except for `docker-compose` package (PRs on how to properly setup apt pinning are welcome, as well as for any other aspect of packaging). Use at your own risk.
