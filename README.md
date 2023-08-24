# DragonflyDB meets Monk

This repository contains Monk.io template to deploy DragonflyDB system either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

- [DragonflyDB meets Monk](#dragonflydb-meets-monk)
  - [Prerequisites](#prerequisites)
    - [Make sure monkd is running](#make-sure-monkd-is-running)
    - [Clone Repository](#clone-repository)
    - [Update configuration](#update-configuration)
    - [Load Template](#load-template)
    - [Verify if it's loaded correctly](#verify-if-its-loaded-correctly)
  - [Deploy DragonflyDB](#deploy-dragonflydb)
  - [Stop, remove and clean up workloads and templates](#stop-remove-and-clean-up-workloads-and-templates)

## Prerequisites

- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

### Make sure monkd is running

```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

### Clone Repository

```bash
git clone git@github.com:monk-io/monk-dragonflydb.git
```

### Update configuration

This template has very basic DragonflyDB configuration and will start a running copy of DragonflyDB, however it is most desired that you would update it with the configuration you would need.
To do so edit the `manifest.yaml` and in the `files` section replace the config provided with yours.
You could also use a `contents: <<< DragonflyDB.conf` notation to read the contents of the file instead of providing it in-line.

### Load Template

```bash
cd monk-dragonflydb
monk load manifest.yaml
```

### Verify if it's loaded correctly

```bash
$ monk list -l dragonflydb
✔ Got the list
Type      Template     Repository  Version  Tags
runnable  dragonflydb/server  local       -        -
```

## Deploy DragonflyDB

```bash
$ monk run dragonflydb/server
✔ Starting the job: local/dragonflydb/server... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% ghcr.io/akafeng/dragonflydb:2.0.9 local
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ Started local/dragonflydb/server

🔩 templates/local/dragonflydb/server
 └─🧊 Peer local
    └─🔩 templates/local/dragonflydb/server
       └─📦 202f7b9e6ac73bb380e9de0464ca4593-local-dragonflydb-server-dragonflydb4
          ├─🧩 ghcr.io/akafeng/dragonflydb:2.0.9
          └─🔌 open tcp 1.1.1.1:179 -> 179

💡 You can inspect and manage your above stack with these commands:
        monk logs (-f) local/dragonflydb/server - Inspect logs
        monk shell     local/dragonflydb/server - Connect to the container's shell
        monk do        local/dragonflydb/server/action_name - Run defined action (if exists)
💡 Check monk help for more!
```

## Stop, remove and clean up workloads and templates

```bash
monk purge    dragonflydb/server
monk purge -x dragonflydb/server
```
