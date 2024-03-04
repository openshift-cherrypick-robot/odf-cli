# odf-cli

The ODF CLI tool provides configuration and troubleshooting commands for OpenShift Data Foundation.

## Commands

- `odf set`:
  - `recovery-profile <profile>`: Set the recovery profile to favor new IO, recovery, or balanced mode with options `high_client_ops`, `high_recovery_ops`, or `balanced`. The default is `balanced`.
  - `ceph log-level <daemon> <subsystem> <log-level>`: Set the log level for Ceph daemons like OSD, mon, mds etc. More information about the ceph subsystems can be found [here](https://docs.ceph.com/en/latest/rados/troubleshooting/log-and-debug/#ceph-subsystems)
- `odf get`:
  - `recovery-profile`: Get the recovery profile value.
  - `health`: Check health of the cluster and common configuration issues.
- `odf purge-osd <ID>`: Permanently remove an OSD from the cluster.
- `odf help` : Display help text
- `odf subvolume ls`: Display all the subvolumes
- `odf subvolume delete <subvolume> <filesystem> <subvolumegroup>`: Deletes the stale subvolumes
- `odf mons`
  - `restore-quorum <monID>`: Restore the mon quorum based on a single healthy mon since quorum was lost with the other mons

## Documentation

Visit docs below for complete details about each command and their flags uses.

- [set](docs/set.md)
- [get](docs/get.md)
- [purge-osd](docs/purge_osd.md)
- [mon](docs/mons.md)

### Root args

These are the arguments that apply to all commands:

- `-h|--help`: this will print brief command help text.

    ```bash
    odf -h
    ```

- `-n|--namespace='openshift-storage'`: the Openshift namespace in which the StorageCluster resides. (optional,  default: openshift-storage)

    ```bash
    odf -n test-cluster [commands]
    ```

- `-o|--operator-namespace` : the Openshift namespace in which the rook operator resides, when the arg `-n` is passed but `-o` is not then `-o` will equal to the `-n`. (default: openshift-storage)

    ```bash
    odf --operator-namespace test-operator -n test-cluster [commands]
    ```

- `--context`: the name of the Openshift context to be used (optional).

    ```bash
    odf --context=$(oc config current-context) [commands]
    ```

## Installation

### Build from source

#### Requirements

- Go >= 1.21
- ODF storage cluster should be installed.

### Build and Run

1. Clone the repository

    ```bash
    git clone https://github.com/red-hat-storage/odf-cli.git
    ```

2. Change the directory and build the binary

    ```bash
    cd odf-cli/ && make build
    ```

3. Use the binary present in the`/bin/` directory to run the commands

    ```bash
    ./bin/odf -h
    ```
