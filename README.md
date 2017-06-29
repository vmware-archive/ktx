# How it works 

The idea is to keep one cluster in one kubernetes config file and soft link the `.kube/config` file between cluster configs.

This script will prevent you from blowing away data inside your `$HOME/.kube/config` file as it checks to make sure that file is a symlink and bails if it is not.

# Installing

## script

    install ktx ~/bin

## PS1

It is very helpful to have your `$PS1` display which cluster is active. You can add `\$(basename \$(readlink $HOME/.kube/config))` to your `$PS1` (in your .bash_profile). 

Note: The backslashes are very important. The bash command will be executed every time it is needed instead of evaluated once and cached.

Here is a sample:

    export PS1="\$(basename \$(readlink $HOME/.kube/config)) \h:\W \u\$ "

# TODO

* bash completion
* list available contexts
* command to save current config if it isn't a symlink