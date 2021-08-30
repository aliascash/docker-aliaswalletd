Building
========

The image can be built from source by running:

        docker build .

A recommended security practice is to add an additional unprivileged user to run the daemon as on the host. For example, as a privileged user, run this on the host:

        useradd aliaswalletd

To build an image which uses this unprivileged user's id and group id, run:

        docker build --build-arg USER_ID=$( id -u aliaswalletd ) --build-arg GROUP_ID=$( id -g aliaswalletd ) .

Now, when the container is run with the default options, the aliaswalletd process will only have the privileges of the aliaswalletd user on the host machine. This is especially important for a process such as aliaswalletd which runs as a network service exposed to the internet.

### Referenced binary release
The build references the Ubuntu 20.04 binaries from the `latest` Github tag. If the build fails, there might be another `latest` release which did not contain the Ubuntu binaries. In that case you need to pass the binary download url as a build argument. Here's an example for the release 4.4.0:

```
docker build --build-arg DOWNLOAD_URL=https://github.com/aliascash/alias-wallet/releases/download/4.4.0/Alias-4.4.0-f1d56b63-Ubuntu-20-04.tgz .
```
