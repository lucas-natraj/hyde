---
layout: post
category : shell
author: Lucas Natraj
tags: [linux, bash]
title: Bash Profile
---

#### ~/.bash_profile

```bash
export PATH=$PATH:/usr/local/bin

# mono / .net
export MONO_MANAGED_WATCHER=disabled
source dnvm.sh

# aliases
alias dm=$(which docker-machine)
alias ve=$(which virtualenv)

# docker
# eval "$(dm env default)"

# shell prompt
PS1="\[\e[0;36m\]\w: \[\e[m\]"
export CLICOLOR=1
export LSCOLORS=cxgxdxdxfxegedabagacad

# dnxmon
function dnxmon() {
    # Run dnx server continuously with nodemon
    # watching for changes to cs or json files
    # Usage:
    #   dnxmon <directory> <command>
    # dnxmon (applies the defaults: current directory and the "web" command)

    function dnxmonFn() {
        nodemon --ext "cs,json" --exec "dnx $1"
    }

    if [[ $# -eq 0 ]]
    then
        echo "running default ..."
        echo "nodemon --ext "cs,json" --exec "dnx web""
        dnxmonFn web
    else
        if [[ $# -eq 1 ]]
        then
            echo "nodemon --ext "cs,json" --exec "dnx $1""
            dnxmonFn $1
        else
            printf "syntax:\n"
            printf "  dnxmon             - will run dnxmon with 'web' as the default command\n"
            printf "  dnxmon <command>   - will run dnxmon with the given command\n"
        fi
    fi
}

# gomon
function gomon() {
    # Run go continuously with nodemon
    # watching for changes to go files
    # Usage:
    #   gomon <directory> <command>
    # gomon (applies the defaults: current directory and app.go)

    function gomonFn() {
        nodemon --ext "go" --exec "$1"
    }

    if [[ $# -eq 0 ]]
    then
        echo "running default ..."
        echo "nodemon --ext "go" --exec "app.go""
        gomonFn app.go
    else
        if [[ $# -eq 1 ]]
        then
            echo "nodemon --ext "go" --exec "$1""
            gomonFn $1
        else
            printf "syntax:\n"
            printf "  dnxmon             - will run dnxmon with 'web' as the default command\n"
            printf "  dnxmon <command>   - will run dnxmon with the given command\n"
        fi
    fi
}

# pymon
function pymon() {
    # Run python continuously with nodemon
    # watching for changes to py files
    # Usage:
    #   pymon <directory> <command>
    # pymon (applies the defaults: current directory and main.py)

    function pymonFn() {
        nodemon --ext "py" --exec "python $1"
    }

    if [[ $# -eq 0 ]]
    then
        echo "running default ..."
        echo "nodemon --ext "py" --exec "python main.py""
        pymonFn main.py
    else
        if [[ $# -eq 1 ]]
        then
            echo "nodemon --ext "py" --exec "python $1""
            pymonFn $1
        else
            printf "syntax:\n"
            printf "  dnxmon             - will run dnxmon with 'web' as the default command\n"
            printf "  dnxmon <command>   - will run dnxmon with the given command\n"
        fi
    fi
}

function py() {
    if [[ $# -eq 1 ]]
    then
        ve "$1"
        source "$1"/bin/activate
    else
        printf "syntax:\n"
        printf "  py <path>             - create a python virtual environment at 'path' and activate it\n"
    fi
}

function py35() {
    if [[ $# -eq 1 ]]
    then
        ve -p /Library/Frameworks/Python.framework/Versions/3.5/bin/python3 --no-site-packages "$1"
        source "$1"/bin/activate
    else
        printf "syntax:\n"
        printf "  py <path>             - create a python virtual environment at 'path' and activate it\n"
    fi
}

function go-here() {
    # update GOPATH to current directory
    export GOPATH=`pwd`
    export PATH=$PATH:$GOPATH/bin
}

function go-init() {
    mkdir -p bin
    mkdir -p pkg
    mkdir -p src
    go-here
}

function ms() {
    export PATH=$PATH:/Users/lnatraj/sdks/azure-cli
    source '/Users/lnatraj/sdks/azure-cli/az.completion'
}

function goog() {
    # go app engine
    export PATH=$PATH:/Users/lnatraj/sdks/go_appengine
    # export PATH=$PATH:/Users/lnatraj/sdks/google-cloud-sdk/platform/google_appengine
    # export PATH=$PATH:/Users/lnatraj/sdks/google-cloud-sdk/platform/google_appengine/goroot/bin
    # export GOROOT=/Users/lnatraj/sdks/google-cloud-sdk/platform/google_appengine/goroot

    # java app engine
    export PATH=$PATH:/Users/lnatraj/sdks/appengine-java-sdk-1.9.38/bin/

    # Update PATH for the Google Cloud SDK.
    # source '/Users/lnatraj/sdks/google-cloud-sdk/path.bash.inc'

    # Enable shell command completion for gcloud.
    # source '/Users/lnatraj/sdks/google-cloud-sdk/completion.bash.inc'

    # The next line updates PATH for the Google Cloud SDK.
    if [ -f '/Users/lnatraj/sdks/google-cloud-sdk/path.bash.inc' ]; then source '/Users/lnatraj/sdks/google-cloud-sdk/path.bash.inc'; fi

    # The next line enables shell command completion for gcloud.
    if [ -f '/Users/lnatraj/sdks/google-cloud-sdk/completion.bash.inc' ]; then source '/Users/lnatraj/sdks/google-cloud-sdk/completion.bash.inc'; fi

    # gradle appengine support
    export APPENGINE_HOME=/Users/lnatraj/sdks/appengine-java-sdk-1.9.38
    export GCLOUD_HOME=/Users/lnatraj/sdks/google-cloud-sdk

    # kubernetes
    alias kub='kubectl'
    source <(kubectl completion bash)
}

# ruby
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*

# bash completion
if [ -f $(brew --prefix)/etc/bash_completion ]; then
  . $(brew --prefix)/etc/bash_completion
fi

# java
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_51.jdk/Contents/Home

# nvm
[[ -s $HOME/.nvm/nvm.sh ]] && . $HOME/.nvm/nvm.sh  # This loads NVM
# Setting PATH for Python 3.6
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.6/bin:${PATH}"

# Setting PATH for Python 3.5
# The original version is saved in .bash_profile.pysave
PATH="/Library/Frameworks/Python.framework/Versions/3.5/bin:${PATH}"

# grpc
PATH="/Users/lnatraj/sdks/protoc-3-3/bin:${PATH}"

```
