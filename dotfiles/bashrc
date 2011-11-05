# gc branch_name -> git checkout branch_name
function gc {
  if [ -z "$1" ]; then
    git checkout master
  else
    git checkout $1
  fi
}

# opens an application from /Applications
function go {
  open "/Applications/$1.app"
}

# todo list manager
# lets you add to .todos or remove-all (kill)
# is displayed on opening bash instance or 'todo show'
function todo {
  if [ -z "$1" ]; then
    echo "what? (call 'todo kill' to remove all tasks)"
    read -e TODO
    echo "echo -e '- $TODO'" >> ~/.todos
  else
    if [ "$1" == "kill" ]; then
      rm ~/.todos
      echo "echo ' '" >> ~/.todos
      echo "tasks removed!"
    else
      . "$HOME/.todos"
    fi
  fi
}

# start app on localhost
# e.g. 'run simfy'
function run {
	if [ "$1" == "simfy" ]; then
	    rvm use ree
	fi
	cd ~/Projects/$1 ; LOG_LEVEL=debug script/server -u
}

function console {
  if [ "$2" == "-c" ]; then
    clear
  fi
  cd ~/Projects/$1 ; script/console
}

# start dev/testing environment
# e.g. 'dev simfy'
function dev {
  if [ "$2" == "-c" ]; then
    clear
  fi
	echo "starting $1..."
	cd ~/Projects/$1
	mate ~/Projects/$1
	if [ "$1" == "simfy" ]; then
	    rvm use ree
	fi
	git log -2
	git status
}

# run with param (folder name of project)
function gg {
  cd ~/Projects/$1
  rake db:test:prepare
  guard
}

# ga filename       -> git add filename
# ga                -> git add .
function ga {
  if [ -z "$1" ]; then
    git add .
  else
    git add $1
  fi
}

# gc branch_name    -> git checkout branch_name
# gc                -> git checkout
function gc {
  if [ -z "$1" ]; then
    git checkout master
  else
    git checkout $1
  fi
}

# repeat a command n times
# usage: repeat 5 echo hello!
function repeat() {
    n=$1
    shift
    while [ $(( n -= 1 )) -ge 0 ]
    do
        "$@"
    done
}

function parse_git_dirty {
  [[ $(git status 2> /dev/null | tail -n1) != "nothing to commit (working directory clean)" ]] && echo "*"
}

function parse_git_branch {
  git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e "s/* \(.*\)/[\1$(parse_git_dirty)]/"
}

export CLICOLOR=1
export LSCOLORS=exfxcxdxbxegedabagacad
export GREP_OPTIONS='--color=auto'
export GREP_COLOR='1;32'

#trap 'echo -ne "."' DEBUG

# color mapping
grey='\[\033[1;30m\]'
red='\[\033[0;31m\]'
RED='\[\033[1;31m\]'
green='\[\033[0;32m\]'
GREEN='\[\033[1;32m\]'
yellow='\[\033[0;33m\]'
YELLOW='\[\033[1;33m\]'
purple='\[\033[0;35m\]'
PURPLE='\[\033[1;35m\]'
white='\[\033[0;37m\]'
WHITE='\[\033[1;37m\]'
blue='\[\033[0;34m\]'
BLUE='\[\033[1;34m\]'
cyan='\[\033[0;36m\]'
CYAN='\[\033[1;36m\]'
NC='\[\033[0m\]'

# this is the magic
export PS1='\[\033[0;37m\]$fill ✈ \t \n\033[1;31m\]$ \u \[\033[1;33m\]\w\[\033[0m\]$(parse_git_branch) \033[1;37m\]✈  \[\033[0m\]'


[[ -s "/Users/pr0xy/.rvm/scripts/rvm" ]] && source "/Users/pr0xy/.rvm/scripts/rvm"  # this loads RVM into a shell session.

trap 'echo -ne "\033[00m"' DEBUG

function prompt_command {
  
  # create a $fill of all screen width minus the time string and a space:
  let fillsize=${COLUMNS}-14
  fill=""
  while [ "$fillsize" -gt "0" ] 
  do
    fill="—${fill}" # fill with underscores to work on
    let fillsize=${fillsize}-1
  done

}

PROMPT_COMMAND=prompt_command


# ascii art welcome stuff
#echo "             ___             "
#echo " _ __  _ __ / _ \__  ___   _ "
#echo "| '_ \| '__| | | \ \/ / | | |"
#echo "| |_) | |  | |_| |>  <| |_| |"
#echo "| .__/|_|   \___//_/\_\\__, |"
#echo "|_|                    |___/ "
#echo ""

# display free disk space on mounted drives
df -hl
