# rdocker
Ravenports package building in Linux Docker containers

Eventually this repository will support two sets of Docker definitions.
The first set supports glibc-based linux (Based on Linux 6.1) package building.
In the future, musl-based linux package building will be supported in a
second set of Docker definition files.

## Debian Docker container instructions

1. Clone this repository or extract an equivalent archive onto a platform with a working Docker system
1. Create localhost directories used by the *ravenports* container
   1. ravenadm profile (default **/srv/rvnprofile**)
   2. full ports tree (default **/srv/specs**)
   3. ccache files (default **/srv/ccache-raven**)
   4. rvn cache files (default **/srv/cache-rvn**)
   5. distribution files case (default **/srv/distfiles**)
   6. ravensource tree (default **/srv/ravensource**)
1. Edit the ___rdocker/ravenports/compose.yaml___ file as necessary.
   1. The webserver listens to port 4040.
   2. ravenadm profile localchost volume
   3. ports tree localhost volume
   4. ccache files localhost volume
   5. rvn cache files localhost volume
1. Edit the ___rdocker/ravenports/ravenports/ravenadm.ini___ configuration as necessary
   1. define max_jobs_per_builder (default **4**)
   2. define number_of_builders (default **6**)
   3. There are many other parameters, but only experts should change them

### Build containers

Container construction takes a little time depending on network connection and server specifications.
```
> cd rdocker/ravenports
> docker-compose build
```

### Run containers

The containers must be detached after start-up.
```
> docker-compose up -d
```

### Interactive with ravenports container

The environment should be ready to immediately build packages at the prompt.
```
> docker exec -it ravenports bash --login
```

### Example build command

The 12-character hash of the prompt is the first part of the container ID.
Before the first build, the ports tree needs to be installed.
```
root@f17ca472f938:/# rvn install ravenports
```

THe following command will build the m4 package set along with any unbuilt dependencies.
```
root@f17ca472f938:/# ravenadm build m4
```
You can check the build logs at http://localhost:4040/ or the external equivalent.

### Leave interactive environment

```
root@f17ca472f938:/# exit
```

### Deactivate containers

It is not necessary to deactivate the containers.  However, the command is:
```
> docker-compose down
```

