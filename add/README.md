## Installation (Linux)

### Manual Installation (Linux)

Since `kubectl-add` are written in Bash, you should be able to install
them to any POSIX environment that has Bash installed.

- Download the `kubectl-add` scripts.
- Either:
  - save them all to somewhere in your `PATH`,
  - or save them to a directory, then create symlinks to `kubectl-add` from somewhere in your `PATH`, like `/usr/local/bin`
- Make `kubectl-add` executable (`chmod +x ...`)

Example installation steps:

``` bash
sudo wget https://raw.githubusercontent.com/EmreDenz/plugins/main/add/kubectl-add
sudo cp kubectl-add /usr/local/bin/kubectl-add
sudo chmod +x kubectl-add
```
USAGE:

  * Adds the values in the data array to the configmap named myconfigmap. If the values in the data already exist, they are replaced.
  kubectl add configmap myconfigmap --data ENVIRONMENT_NAME:VALUE -s ENVIRONMENT_NAME2:VALUE2 -f -n default

  * Adds the values in the data array to the configmap named myconfigmap in default namespace. If the values in the data already exist, they are not replaced.
  kubectl add configmap myconfigmap --data ENVIRONMENT_NAME:VALUE -s ENVIRONMENT_NAME2:VALUE2 -n default

  * Adds the values in the data array to the secret named mysecret in default namespace. If the values in the data already exist, they are replaced. Encrypts values with base64
  kubectl add secret mysecret --data ENVIRONMENT_NAME:VALUE -s ENVIRONMENT_NAME2:VALUE2 -f -n default -b

  kubectl add TYPE NAME DATA [options]

  Describe Commands:
  TYPE                       : configuration type. configmap(cm), secret
  NAME                       : name of the configuration
  DATA                       : list of data to add/replace. (--set, -s)

  Options:

  -n, --namespace: namespace.
  -f, --force: If key exists, the values is replaced.
  -e, --encode-base64: values are base64 encoded.
  -d, --decode-base64: values are base64 decoded.
