# ktx

## Overview

Managing kubeconfig files can become tedious when you have multiple clusters and contexts to switch between. `ktx` aims to reduce friction caused by switching between various configurations.

`ktx` takes the approach of modifying the `KUBECONFIG` environment variable to select the desired config.

## Getting Started

### Prerequisites

* Your shell is bash or zsh.
* `git` is installed.

### Install

```sh
# clone the ktx repo
git clone https://github.com/heptio/ktx
cd ktx

# Install the bash function
cp ktx "${HOME}"/.ktx

# Add this to your "${HOME}/".bash_profile (or similar)
source "${HOME}"/.ktx

# Install the auto-completion
cp ktx-completion.sh "${HOME}"/.ktx-completion.sh

# Add this to your "${HOME}/".bash_profile (or similar)
source "${HOME}"/.ktx-completion.sh

# Reload your shell
exec bash
```

### Usage

Once `ktx` is installed you can use it as auto-complete:

```sh
$ kubectl get po
The connection to the server localhost:8080 was refused - did you specify the right host or port?
# useful to see what clusters you have in ${HOME}/.kube/
$ ktx <tab><tab>
alpha beta gamma delta epsilon
$ ktx gamma
$ kubectl get po
No resources found.
```

## Optional Bells & Whistles

### PS1

It is helpful to display the active cluster in the command prompt.

![shows the cluster name in the command prompt](/ss.png?raw=true "ktx in action")

### Steps

1. Find out what the current value of `PS1`: `echo "${PS1}"`
2. Put `"\$(basename \${KUBECONFIG:=\"\"})" ` in front of the existing value of `PS1`

Note: The backslashes are very important. This tells bash to re-evaluate every time instead of once on load.

### Example

```sh
salazar:ktx cha$ echo "${PS1}"
\h:\W \u$

# inside .bash_profile
export PS1="\$(basename \${KUBECONFIG:=\"\"}) \h:\W \u$ "

# Reload your shell
exec bash
```

# Pronunciation Guide

`ktx` is pronounced as "k thanks"
