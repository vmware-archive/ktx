# How it works

The idea is to keep one cluster in one kubernetes config file and have an easy way to switch between clusters.

Since you may want several environments (terminals) configured for different clusters we want to use the `KUBECONFIG` environment variable to identify the configured cluster.

# Installation

## script

    install ktx ~/bin

## PS1

It is very helpful to have your `$PS1` display which cluster is active. You can add `\$(basename \${KUBECONFIG})` to your `$PS1` (in your .bash_profile).

Note: The backslashes are very important. The bash command will be executed every time it is needed instead of evaluated once and cached.

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
