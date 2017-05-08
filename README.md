# Web app using Go


## Installation and initial setup

- Install Go (look up internet - pretty simple)
- Set up environment variables (GOPATH=<your code worspace> and GOROOT=<which go>)
- Example below
```
# On a mac
echo 'export GOPATH=$HOME/Code/go' >> ~/.bash_profile
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bash_profile
source ~/.bash_profile
mkdir -p ~/Code/go/src/github.com/machzqcq/go-experiments
```
- I set up my GOPATH=/Users/pmacharl/code/go and GOROOT=/usr/local/go (this was already set while installation)
- From shell/command line type `go env` - You should be able to see the environment variables

## Workspaces
As you continue working - you will quickly realize that you need multiple workspaces/projects i.e. you would not want to put your source code always in the Global GOPATH ($HOME/Code/go) as I declared above. There are two ways to deal with it

- Option1: By default you can simply have multiple paths defined in your GOPATH and Go looks for src in all folders in that order (So lets say you can have your global , private, work etc.). 
- Option2: Everytime your cd into the root of your projet (think of github project for e.g.), then initialize GOPATH. So essentially override the 'cd' command for bash shell and drop in a .gopath empty file in the root of every folder/project. That way the cd will append your current root of folder to GOTPATH. I had this in my ~/.bash_profile and a .gopath in the root of every go project where my 'src' resides

```
cd () {
    builtin cd "$@"
    cdir=$PWD
    while [ "$cdir" != "/" ]; do
        if [ -e "$cdir/.gopath" ]; then
            export GOPATH=$cdir # GOPATH=$GOPATH:$cdir if you want to preserve existing
            break
        fi
        cdir=$(dirname "$cdir")
    done
}
```  

Note: If you are using vscode, then your integrated terminal executes .bashrc, hence include the above in .bashrc as well

- Related info: This might be the most closest to many developers who know RVM, pyvm, virtualenv etc. Here is the [gvm](https://github.com/moovweb/gvm) (go version manager). This lets you define multiple GOROOT (i.e. multiple Go runtimes) and manage multiple GOPATHs with gvm pkgset. Read the full documentation


## To install local assets:

* install NodeJs (https://nodejs.org)
* install `grunt-cli` globally via `npm install -g grunt-cli`
* run `npm install` from the root directory of the project
* run `grunt` from the root directory of the project to compile CSS

To run the application:
* install the app with `go install github.com/lss/webapp`
* run with `bin/webapp`
* navigate to `http://localhost:8000/html/home.html`

