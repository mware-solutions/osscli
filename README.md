# Object Storage Client Quickstart Guide

Provides a modern alternative to UNIX commands like ls, cat, cp, mirror, diff, find etc. It supports filesystems and Amazon S3 compatible cloud storage service (AWS Signature v2 and v4).

```
ls        list buckets and objects
mb        make a bucket
rb        remove a bucket
cat       display object contents
head      display first 'n' lines of an object
pipe      stream STDIN to an object
share     generate URL for temporary access to an object
cp        copy objects
mirror    synchronize objects to a remote site
find      search for objects
sql       run sql queries on objects
stat      stat contents of objects
lock      set and get object lock configuration
retention set object retention for objects with a given prefix
legalhold set object legal hold for objects
diff      list differences in object name, size, and date between buckets
rm        remove objects
event     manage object notifications
watch     watch for object events
policy    manage anonymous access to objects
admin     manage MinIO servers
session   manage saved sessions for cp command
config    manage mc configuration file
update    check for a new software update
version   print version info
```

## Install from Source
Source installation is only intended for developers and advanced users. If you do not have a working Golang environment, please follow [How to install Golang](https://golang.org/doc/install). Minimum version required is [go1.13](https://golang.org/dl/#stable)

```sh
GO111MODULE=on go get github.com/mware-solutions/osscli
```

## Add a Cloud Storage Service
If you are planning to use `mc` only on POSIX compatible filesystems, you may skip this step and proceed to [everyday use](#everyday-use).

To add one or more Amazon S3 compatible hosts, please follow the instructions below. `mc` stores all its configuration information in ``~/.mc/config.json`` file.

```
osscli config host add <ALIAS> <YOUR-S3-ENDPOINT> <YOUR-ACCESS-KEY> <YOUR-SECRET-KEY> --api <API-SIGNATURE> --lookup <BUCKET-LOOKUP-TYPE>
```

Alias is simply a short name to your cloud storage service. S3 end-point, access and secret keys are supplied by your cloud storage provider. API signature is an optional argument. By default, it is set to "S3v4".

Lookup is an optional argument. It is used to indicate whether dns or path style url requests are supported by the server. It accepts "dns", "path" or "auto" as valid values. By default, it is set to "auto" and SDK automatically determines the type of url lookup to use.

### Example - BDL Cloud Storage
BDL server displays URL, access and secret keys.

```
osscli config host add bdl https://storage-19986925976585.cloud.bigconnect.io 19986925976585 19986925976585
```

<a name="everyday-use"></a>
## Everyday Use

### Shell aliases
You may add shell aliases to override your common Unix tools.

```
alias ls='osscli ls'
alias cp='osscli cp'
alias cat='osscli cat'
alias mkdir='osscli mb'
alias pipe='osscli pipe'
alias find='osscli find'
```

### Shell autocompletion
In case you are using bash, zsh or fish. Shell completion is embedded by default in `osscli`, to install auto-completion use `osscli --autocompletion`. Restart the shell, osscli will auto-complete commands as shown below.

```
osscli <TAB>
admin    config   diff     find     ls       mirror   policy   session  sql      update   watch
cat      cp       event    head     mb       pipe     rm       share    stat     version
```

# Build
buildscripts/build.sh

