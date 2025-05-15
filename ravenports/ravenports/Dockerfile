# Corresponds to Linux 6.1
FROM debian:bookworm-slim

# Get downloader
ADD https://www.ravenports.com/repository/ravenports-downloader.sh downloader.sh

# install wget
RUN apt-get update \
    && apt-get install -y wget \
    && apt-get install -y lsof \
    && apt-get install -y binutils

# Install Ravenports
RUN bash downloader.sh

# Add /raven to sudo paths
RUN echo "Defaults  secure_path = /sbin:/bin:/usr/sbin:/usr/bin:/raven/sbin:/raven/bin" >> /etc/sudoers

# Add /raven paths to $PATH
RUN echo "PATH=\$PATH:/raven/sbin:/raven/bin" > /etc/profile.d/searchraven.sh

# Install Ravenports
RUN /raven/sbin/rvn install -y ravenports~

# Wait to update to latest release - mappings not available during build
RUN find /var/cache/rvn ! -type d -delete

# Overwrite configuration
COPY ravenadm.ini /raven/etc/ravenadm/ravenadm.ini

# Forever command to keep container running for interactive use
ENTRYPOINT ["tail", "-f", "/dev/null"]
