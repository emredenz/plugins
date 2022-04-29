# Power tools for kubectl and helm

![Latest GitHub release](https://img.shields.io/github/release/EmreDenz/plugins.svg)
![GitHub stars](https://img.shields.io/github/stars/EmreDenz/plugins.svg?label=github%20stars)
![Proudly written in Bash](https://img.shields.io/badge/written%20in-bash-ff69b4.svg)

What are tools?

kubectl-add is a tool for quickly adding data to configmap and secret in kubectl.

### Examples

```sh
# adding new data to configmap
$ kubectl add configmap myconfigmap -s mykey:myvalue -n mynamespace
The mykey is adding.
configmap/myconfigmap replaced

# adding new multidata to configmap
$ kubectl add cm myconfigmap -s mykey2:myvalue2 -s mykey3:myvalue3 -n mynamespace
The mykey2 is adding.
The mykey3 is adding.
configmap/myconfigmap replaced

# if data already exists when adding data to configmap
$ kubectl add configmap myconfigmap -s mykey3:myvalue3 -s mykey4:value4  -n mynamespace
error: The mykey3 is already exist.

# adding data to configmap with force argument
$ kubectl add configmap myconfigmap -s mykey3:myvalue3 -s mykey4:value4  -n mynamespace -f
The mykey3 is already exist, is updating.
The mykey4 is adding.
configmap/myconfigmap replaced

# adding data by decoding it.
$ kubectl add configmap myconfigmap -s mykey5:bXl2YWx1ZTU=  -n mynamespace -d
The mykey5 is adding.
configmap/myconfigmap replaced

# adding new data to secret
$ kubectl add mysecret mysecret -s mykey:bXl2YWx1ZQ== -n mynamespace
The mykey2 is adding.
secret/mysecret replaced

# adding new data to secret without value is not in base64 format
$ kubectl add mysecret mysecret -s mykey2:randomvalue -n mynamespace
The mykey2 is adding.
error: the input does not conform to the base64 format.

```

Along with kubectl-add it supports directly adding or updating new data without editing configmap and secret. It supports encode or decode with given base64 when appending data.

-----

## Installation

Stable versions of kubectl-add is small bash scripts that you can find in this repository.

Installation options:

- [as kubectl plugins (Linux)(Manual)](#kubectl-plugins-linux)

### Kubectl Plugins (Linux)

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
sudo chmod +x /usr/local/bin/kubectl-add
```

### USAGE:

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
