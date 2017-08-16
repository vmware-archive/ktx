# How it works

The idea is to keep one cluster in one kubernetes config file and have an easy way to switch between clusters.

Since you may want several environments (terminals) configured for different clusters we want to use the `KUBECONFIG` environment variable to identify the configured cluster.

# Installation

## Prerequisites

0. Your shell is bash.
1. `${HOME}/bin` exists and is in your `${PATH}`.
2. You have `curl` installed
3. You have `git` installed

## From github

    # clone this repo
    git clone https://github.com/heptio/ktx
    cd ktx

    # Install the script
    install ktx ${HOME}/bin

    # Install the autocompletion
    cp ktx-completion.sh ${HOME}/.ktx-completion.sh
    # Add this to your `${HOME}/.bash_profile
    source ${HOME}/.ktx-completion.sh

    # Reload your shell
    exec bash

## PS1

It is very helpful to have your command prompt display which cluster is active. Add `\$(basename \${KUBECONFIG})` to your `${PS1}` (in your `${HOME}/.bash_profile`) to enable this feature.

Note: The backslashes are very important. This tells bash to re-evaluate every time instead of once on load.

Here is a sample:

    export PS1="\$(basename \${KUBECONFIG}) \h:\W \u\$ "

# Usage

Once `ktx` is installed you can use it as autocomplete:

    # useful to see what clusters you have in ${HOME}/.kube/
    $ ktx <tab><tab>
    alpha beta gamma delta epsilon
    $ ktx gamma
    export KUBECONFIG=/home/you/.kube/gamma
    # Actually set the environment variable
    $ eval $(ktx gamma)

# TODO: Document how to customize
