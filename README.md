# Rocket.Chat server -- Ubuntu 18.04 ansible role

This ansible role is directly based on the official (non-working)
[RocketChat ansible role](https://github.com/RocketChat/Rocket.Chat.Ansible).

It deploys only the RocketChat server (see the [RocketChat mongodb
role](https://github.com/pgaxatte/ansible_rocket_mongodb) for the mongodb part) and only works on Ubuntu
18.04.

## Role Variables

All defaults are set in [`defaults/main.yml`](defaults/main.yml)

### RocketChat configuration

|     Name     |     Default Value    |    Description     |
|---------------------------|-----------------------|------------------------------------|
| `rocket_chat_automatic_upgrades` | true | A boolean value that determines whether or not to upgrade Rocket.Chat upon source code changes |
| `rocket_chat_upgrade_backup` | true | A boolean value that determines whether or not to back up the current Rocket.Chat version when upgrading |
| `rocket_chat_upgrade_backup_path` | `"{{ rocket_chat_application_path }}"`| The path to store the back up of Rocket.Chat when `rocket_chat_upgrade_backup` is `true` |
| `rocket_chat_application_path` | `/var/lib/rocket.chat` | The destination on the filesystem to deploy Rocket.Chat to |
| `rocket_chat_version` | `latest` | The version of Rocket.Chat to deploy; see the [Rocket.Chat releases page](https://rocket.chat/releases) for available options |
| `rocket_chat_tarball_remote` | See [`defaults/main.yml`](defaults/main.yml) | The remote URL to fetch the Rocket.Chat tarball from (uses `rocket_chat_version`) |
| `rocket_chat_tarball_sha256sum` | See [`defaults/main.yml`](defaults/main.yml) | The SHA256 hash sum of the Rocket.Chat tarball being fetched |
| `rocket_chat_tarball_fetch_timeout` | 100 | The time (in seconds) before the attempt to fetch the Rocket.Chat tarball fails |
| `rocket_chat_tarball_validate_remote_cert` | true | A boolean value that determines wether or not to validate the SSL certs for the Rocket.Chat tarball remote |
| `rocket_chat_service_user` | `rocketchat` | The name of the user that will run the Rocket.Chat server process |
| `rocket_chat_service_group` | `rocketchat` | The name of the primary group for the `rocket_chat_service_user` user |
| `rocket_chat_service_host` | `"{{ ansible_fqdn }}"` | The FQDN of the Rocket.Chat system |
| `rocket_chat_service_port` | 3000 | The TCP port Rocket.Chat listens on |
| `rocket_chat_service_extra_instances` | `[]` | List of TCP port numbers for additional rocketchat service instances to handle more users on one machine |
| `rocket_chat_node_version` | `12.18.4` | The version of NodeJS to install that `n` understands |
| `rocket_chat_node_prefix` | `/usr/local/n/versions/node/{{ rocket_chat_node_version }}` | The path to the `node` binary directory that n installs |
| `rocket_chat_npm_version` | `6.14.0` | The version of NodeJS to install that `n` understands |
| `rocket_chat_npm_dist` | `/usr/bin/npm` | The path to the original `npm` binary, before n installs any Node versions |

### MongoDB connection configuration

|     Name     |     Default Value    |    Description     |
|---------------------------|-----------------------|------------------------------------|
| `rocket_chat_mongodb_user` | not used by default | Username to be used when connecting to MongoDB. If you set this, you should also define `rocket_chat_mongodb_password`, otherwise no user/pass is used to connect to MongoDB |
| `rocket_chat_mongodb_password` | not used by default | Password to be used when connecting to MongoDB. If you set this, you should also define `rocket_chat_mongodb_user`, otherwise no user/pass is used to connect to MongoDB |
| `rocket_chat_mongodb_server` | 127.0.0.1 | The IP/FQDN of the MongoDB host |
| `rocket_chat_mongodb_port` | 27017 | The TCP port to contact the MongoDB host host via |
| `rocket_chat_mongodb_database` | rocketchat |  The MongoDB database to be used for Rocket.Chat |
| `rocket_chat_mongodb_use_tls`   | false  | Whether or not to use TLS to connect to the MongoDB DB  |
