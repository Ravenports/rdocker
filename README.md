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
1. Edit the ravenports/compose.yaml file as necessary.
   1. The webserver listens to port 4040.
   2. ravenadm profile localchost volume
   3. ports tree localhost volume
   4. ccache files localhost volume
   5. rvn cache files localhost volume
1. Edit the ravenports/ravenports/ravenadm.ini configuration as necessary
   1. define max_jobs_per_builder (default **8**)
   2. define number_of_builders (default **12**)
