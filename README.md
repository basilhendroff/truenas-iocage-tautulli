# freenas-iocage-tautulli
This is a simple script to automate the installation of Tautulli in a FreeNAS jail. It will create a jail, install the latest version of Tautulli for FreeBSD from [tautulli.com](https://www.tautulli.com), and store its configuration data outside the jail.  

## Status
This script will work with FreeNAS 11.3, and it should also work with TrueNAS CORE 12.0. Due to the EOL status of FreeBSD 11.2, it is unlikely to work reliably with earlier releases of FreeNAS.

## Usage
A python based web application for monitoring, analytics and notifications for Plex Media Server

### Prerequisites

Although not required, it's recommended to create a Dataset named `apps` with a sub-dataset named `tautulli` on your main storage pool.  Many other jail guides also store their configuration and data in subdirectories of `pool/apps/` If this dataset is not present, directory `/apps/tautulli` will be created in `$POOL_PATH`.

### Installation

Download the repository to a convenient directory on your FreeNAS system by changing to that directory and running `git clone https://github.com/basilhendroff/freenas-iocage-tautulli`. Then change into the new freenas-iocage-tautulli directory and create a file called tautulli-config with your favorite text editor. In its minimal form, it would look like this:

```
JAIL_IP="10.1.1.3"
DEFAULT_GW_IP="10.1.1.1"
```

Many of the options are self-explanatory, and all should be adjusted to suit your needs, but only a few are mandatory. The mandatory options are:

- JAIL_IP is the IP address for your jail. You can optionally add the netmask in CIDR notation (e.g., 192.168.1.199/24). If not specified, the netmask defaults to 24 bits. Values of less than 8 bits or more than 30 bits are invalid.
- DEFAULT_GW_IP is the address for your default gateway

In addition, there are some other options which have sensible defaults, but can be adjusted if needed. These are:

- JAIL_NAME: The name of the jail, defaults to `tautulli`.
- POOL_PATH: The path for your data pool. It is set automatically if left blank.
- CONFIG_PATH: Client configuration data is stored in this path; defaults to `$POOL_PATH/apps/tautulli`.
- INTERFACE: The network interface to use for the jail. Defaults to `vnet0`.
- VNET: Whether to use the iocage virtual network stack. Defaults to `on`.

### Execution

Once you've downloaded the script and prepared the configuration file, run this script (`./tautulli-jail.sh`). The script will run for several minutes. When it finishes, your jail will be created and Tautulli will be installed.

### Test

To test your installation, enter your Tautulli jail IP address and port 8181 e.g. `10.1.1.3:8181` in a browser. If the installation was successful, you should see a Tautulli login screen.

## Support and Discussion

There are several support streams for Tautulli including the Tautulli website, Reddit, Discord and Plex forums. They call all be accessed from the [Tautulli support portal](https://tautulli.com/#support).

Questions or issues about this resource can be raised in [this forum thread]().  


