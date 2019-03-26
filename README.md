# bashrc
 
``` 
# Source global definitions
if [ -f /etc/bashrc ]; then
  . /etc/bashrc
fi

alias cp='cp -i'
# alias ct='cleartool'
alias h='history'
alias l='ls -hal'
alias mkdir='mkdir -p'
alias mv='mv -i'
alias original='original'
alias mv='mv -i'
# alias pipinstall='pip install --index-url=http://pypi.python.org/simple/ --trusted-host pypi.python.org'
alias rgrep='find . | xargs grep'
alias rm='rm -i'
# alias vi='/usr/bin/vim'
if [ "`/usr/bin/whoami`" == "root" ]; then
  PS1='\[\033]0;\h:\w\007\033[01;31m\]\u@\h \[\033[01;31m\033[0m\]# '
else
  PS1='\[\033]0;\h:\w\007\033[32m\]\u@\h \[\033[33m\033[0m\]$ '
fi

export PS1;
export HISTTIMEFORMAT="%y-%m-%d %T  "

original() {
  SRC=$1
  if [ -z $SRC ]; then
    print "Enter a source file to backup as an original (*.ORIGINAL)"
    exit 0
  fi
  ls $SRC.ORIGINAL > /dev/null
  if [ "$?" -eq "0" ]; then
    echo "$SRC.ORIGINAL already exists."
  else 
    mv $SRC $SRC.ORIGINAL
    cp $SRC.ORIGINAL $SRC
  fi
  ls -l $SRC*
}

alias original='original'

createbash() {
  SRC=$1
  if [ -z $SRC ]; then
    print "Enter a name for the shell script."
    exit 0
  fi
  ls $SRC > /dev/null
  if [ "$?" -eq "0" ]; then
    echo "$SRC already exists."
  else
    echo "Creating file $SRC"
    echo '#!/bin/bash'>$SRC
    echo 'SCRIPT_NAME="$(basename "$0")"'>>$SRC
    echo 'WKDIR="$(dirname "$0")"'>>$SRC
    chmod 755 $SRC
  fi 
}

alias createbash='createbash'

TERM=xterm; export TERM
SHELL=/bin/bash; export SHELL
``` 
