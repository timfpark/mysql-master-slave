# MySQL

[Helm](https://helm.sh/) chart to deploy a multi-pod MySQL master-slave deployment [Kubernetes](http://kubernetes.io) cluster. Work was largely inspired by this [tutorial](https://kubernetes.io/docs/tutorials/stateful-application/run-replicated-stateful-application/).

## Usage

### Install 

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release stable/mysql
```

The command deploys MySQL cluster on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

### Uninstall

To uninstall/delete the `my-release` deployment:

```bash
$ helm delete my-release
```

## Configuration

The following tables lists the configurable parameters of the MySQL chart and their default values.

| Parameter                  | Description                        | Default                                                    |
| -----------------------    | ---------------------------------- | ---------------------------------------------------------- |
| `imageTag`                 | `mysql` image tag.                 | Most recent release                                        |
| `mysqlRootPassword`        | Password for the `root` user.      | `nil`                                                      |
| `mysqlUser`                | Username of new user to create.    | `nil`                                                      |
| `mysqlPassword`            | Password for the new user.         | Randomly generated                                         |
| `mysqlDatabase`            | Name for new database to create.   | `nil`                                                      |
| `persistence.size`         | Size of persistent volume claim    | 10Gi
| `persistence.storageClass` | Type of persistent volume claim    | fast
| `persistence.accessMode`   | ReadWriteOnce or ReadOnly          | ReadWriteOnce                                              |
| `resources`                | CPU/Memory resource requests/limits | Memory: `256Mi`, CPU: `100m`                              |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set mysqlLRootPassword=secretpassword,mysqlUser=my-user,mysqlPassword=my-password,mysqlDatabase=my-database \
    stable/mysql
```

The above command sets the MySQL `root` account password to `secretpassword`. Additionally it creates a standard database user named `my-user`, with the password `my-password`, who has access to a database named `my-database`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml stable/mysql
```