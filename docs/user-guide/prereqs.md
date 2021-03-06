---
assignees:
- bgrant0607
- mikedanese
title: Installing and Setting up kubectl
redirect_from:
- "/docs/getting-started-guides/kubectl/"
- "/docs/getting-started-guides/kubectl.html"
---

To deploy and manage applications on Kubernetes, you'll use the
Kubernetes command-line tool, [kubectl](/docs/user-guide/kubectl/). It
lets you inspect your cluster resources, create, delete, and update
components, and much more. You will use it to look at your new cluster
and bring up example apps.

You should use a version of kubectl that is at least as new as your
server.  `kubectl version` will print the server and client versions.
Using the same version of kubectl as your server naturally works;
using a newer kubectl than your server also works; but if you use an
older kubectl with a newer server you may see odd validation errors.

Here are a few methods to install kubectl.

## Install kubectl Binary Via curl

Download the latest release with the command:

```shell
# OS X
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl

# Linux
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

# Windows
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/windows/amd64/kubectl.exe
```

If you want to download a specific version of kubectl you can replace the nested curl command from above with the version you want. (e.g. v1.4.6, v1.5.0-beta.2)

Make the kubectl binary executable and move it to your PATH (e.g. `/usr/local/bin`):

```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

## Extract kubectl from Release .tar.gz or Compiled Source

If you downloaded a pre-compiled [release](https://github.com/kubernetes/kubernetes/releases), kubectl will be under `platforms/<os>/<arch>` from the tar bundle.

If you compiled Kubernetes from source, kubectl should be either under `_output/local/bin/<os>/<arch>` or `_output/dockerized/bin/<os>/<arch>`.

Copy or move kubectl into a directory already in your PATH (e.g. `/usr/local/bin`). For example:

```shell
# OS X
sudo cp platforms/darwin/amd64/kubectl /usr/local/bin/kubectl

# Linux
sudo cp platforms/linux/amd64/kubectl /usr/local/bin/kubectl
```

Next make it executable with the following command:

```shell
sudo chmod +x /usr/local/bin/kubectl
```

The kubectl binary doesn't have to be installed to be executable, but the rest of the walkthrough will assume that it's in your PATH.

If you prefer not to copy kubectl, you need to ensure it is in your path:

```shell
# OS X
export PATH=<path/to/kubernetes-directory>/platforms/darwin/amd64:$PATH

# Linux
export PATH=<path/to/kubernetes-directory>/platforms/linux/amd64:$PATH
```

## Download as part of the Google Cloud SDK

kubectl can be installed as part of the Google Cloud SDK:

First install the [Google Cloud SDK](https://cloud.google.com/sdk/).

After Google Cloud SDK installs, run the following command to install `kubectl`:

```shell
gcloud components install kubectl
```

Do check that the version is sufficiently up-to-date using `kubectl version`.

## Install with brew

If you are on MacOS and using brew, you can install with:

```shell
brew install kubectl
```

The homebrew project is independent from kubernetes, so do check that the version is
sufficiently up-to-date using `kubectl version`.

## Configuring kubectl

In order for kubectl to find and access the Kubernetes cluster, it needs a [kubeconfig file](/docs/user-guide/kubeconfig-file), which is created automatically when creating a cluster using kube-up.sh (see the [getting started guides](/docs/getting-started-guides/) for more about creating clusters). If you need access to a cluster you didn't create, see the [Sharing Cluster Access document](/docs/user-guide/sharing-clusters).
By default, kubectl configuration lives at `~/.kube/config`.

#### Making sure you're ready

Check that kubectl is properly configured by getting the cluster state:

```shell
$ kubectl cluster-info
```

If you see a url response, you are ready to go.

## Enabling shell autocompletion

kubectl includes autocompletion support, which can save a lot of typing!

The completion script itself is generated by kubectl, so you typically just need to invoke it from your profile.

Common examples are provided here, but for more details please consult `kubectl completion -h`

### On Linux, using bash

To add it to your current shell: `source <(kubectl completion bash)`

To add kubectl autocompletion to your profile (so it is automatically loaded in future shells):

```shell
echo "source <(kubectl completion bash)" >> ~/.bashrc
```

### On MacOS, using bash

On MacOS, you will need to install the bash-completion support first:

```shell
brew install bash-completion
```

To add it to your current shell:

```shell
source $(brew --prefix)/etc/bash_completion
source <(kubectl completion bash)
```

To add kubectl autocompletion to your profile (so it is automatically loaded in future shells):

```shell
echo "source $(brew --prefix)/etc/bash_completion" >> ~/.bash_profile
echo "source <(kubectl completion bash)" >> ~/.bash_profile
```

Please note that this only appears to work currently if you install using `brew install kubectl`,
and not if you downloaded kubectl directly.

## What's next?

[Learn how to launch and expose your application.](/docs/user-guide/quick-start)
