#     /$$   /$$                                   /$$$$$$ /$$$$$$$$
#    | $$  | $$                                  |_  $$_/|__  $$__/
#    | $$  | $$  /$$$$$$   /$$$$$$  /$$$$$$/$$$$   | $$     | $$   
#    | $$$$$$$$ /$$__  $$ /$$__  $$| $$_  $$_  $$  | $$     | $$   
#    | $$__  $$| $$$$$$$$| $$$$$$$$| $$ \ $$ \ $$  | $$     | $$   
#    | $$  | $$| $$_____/| $$_____/| $$ | $$ | $$  | $$     | $$   
#    | $$  | $$|  $$$$$$$|  $$$$$$$| $$ | $$ | $$ /$$$$$$   | $$   
#    |__/  |__/ \_______/ \_______/|__/ |__/ |__/|______/   |__/   
#                                                                  
#    Mark Heemskerk - mark@heemit.nl
#
# .bashrc
#
# 1. GENERAL
# 2. ALIASES
# 3. FUNCTIONS
# 4. ENVIRONMENTS
# 5. HISTORY
# 6. PROMPT

###################################################################
# 1. GENERAL
###################################################################
iatest=$(expr index "$-" i)

# Source global definitions
if [ -f /etc/bashrc ]; then
	. /etc/bashrc
fi

# Use fastfetch if available
if [ -f /usr/bin/fastfetch ]; then
	fastfetch
fi

# Enable bash programmable completion features in interactive shells
if [ -f /usr/share/bash-completion/bash_completion ]; then
	. /usr/share/bash-completion/bash_completion
elif [ -f /etc/bash_completion ]; then
	. /etc/bash_completion
fi

# Disable the bell sound
if [[ $iatest -gt 0 ]]; then bind "set bell-style none"; fi

# Check the window size after each command and, if necessary,
shopt -s checkwinsize

# Enable colors
force_color_prompt=yes

# Vim key-bindings
set -o vi

# Correct minor spelling errors in cd
shopt -s cdspell
# Include dotfiles in wildcard expansion, and match case-insensitively
shopt -s dotglob
shopt -s nocaseglob

# Allow ctrl-S for history navigation (with ctrl-R)
[[ $- == *i* ]] && stty -ixon

# Ignore case on auto-completion
# Note: bind used instead of sticking these in .inputrc
if [[ $iatest -gt 0 ]]; then bind "set completion-ignore-case on"; fi

# Show auto-completion list automatically, without double tab
if [[ $iatest -gt 0 ]]; then bind "set show-all-if-ambiguous On"; fi

###################################################################
# 2. ALIASES
###################################################################
# Better GNU utils with colors
alias ls='ls --color=auto'
alias ll='ls -laht --color=always'
alias less='less -R'
alias mkdir='mkdir -p'
alias grep='grep --color=auto'
# Most used locations
alias infra='cd ~/git/ansible/infra_vars'
# To avoid mistakes
alias rm='rm -i'
alias cp='cp -i'
alias mv='mv -i'
# Easy cd
alias ..='cd ..'
alias ...='cd ../../../'
alias ....='cd ../../../../'
alias .....='cd ../../../../'
# File search
alias ff='find . -type f -iname'
alias fd='find . -type d -iname'
# Alias to show the date
alias da='date "+%Y-%m-%d_%H:%M"'
# Better tree
alias tree='tree -CAhF --dirsfirst'

###################################################################
# 3. FUNCTIONS
###################################################################
# Revert back to main/master
# Usage: revert main
function revert(){
      git reset --hard $1
    }

# Useful unarchiver
# Usage: extract dir.tar
function extract () {
        if [ -f $1 ] ; then
                case $1 in
                        *.tar.bz2)        tar xjf $1                ;;
                        *.tar.gz)        tar xzf $1                ;;
                        *.bz2)                bunzip2 $1                ;;
                        *.rar)                rar x $1                ;;
                        *.gz)                gunzip $1                ;;
                        *.tar)                tar xf $1                ;;
                        *.tbz2)                tar xjf $1                ;;
                        *.tgz)                tar xzf $1                ;;
                        *.zip)                unzip $1                ;;
                        *.Z)                uncompress $1        ;;
                        *)                        echo "'$1' cannot be extracted via extract()" ;;
                esac
        else
                echo "'$1' is not a valid file"
        fi
}

# Goes up a specified number of directories
# Usage: up 4
up() {
	local d=""
	limit=$1
	for ((i = 1; i <= limit; i++)); do
		d=$d/..
	done
	d=$(echo $d | sed 's/^\///')
	if [ -z "$d" ]; then
		d=..
	fi
	cd $d
}

# Searches for text in all files in the current folder
# Usage: grept STRING_TO_SEARCH
grept() {
	# -i case-insensitive
	# -I ignore binary files
	# -H causes filename to be printed
	# -r recursive search
	# -n causes line number to be printed
	# optional: -F treat search term as a literal, not a regular expression
	# optional: -l only print filenames and not the matching lines ex. grep -irl "$1" *
	grep -iIHrn --color=always "$1" . | less -r
}

# Improved cd command that lists directory after changing
cd() {
    builtin cd "$@" && ls -la
}

# --- Color Definitions (Add these if not already present) ---
ECHO_RESET='\033[0m'
ECHO_BOLD_YELLOW='\033[1;33m'
ECHO_BOLD_GREEN='\033[1;32m'
ECHO_RED='\033[1;31m'

# Function to display cheatsheet for common commands
# Usage: cheatsheet git
cheatsheet() {
    local command="$1"
    
    # If no argument provided, show available options
    if [ -z "$command" ]; then
        echo -e "${ECHO_BOLD_YELLOW}Available cheatsheets:${ECHO_RESET} git, bash, vim, tmux, aliases, functions"
        return
    fi
    
    case "$command" in
        git)
            echo -e "${ECHO_BOLD_GREEN}Git Cheatsheet:${ECHO_RESET}"
            echo -e "${ECHO_YELLOW}git init${ECHO_RESET}                    - Initialize a repository"
            echo -e "${ECHO_YELLOW}git clone [url]${ECHO_RESET}               - Clone a repository"
            echo -e "${ECHO_YELLOW}git add [file]${ECHO_RESET}                - Add file to staging"
            echo -e "${ECHO_YELLOW}git commit -m [msg]${ECHO_RESET}           - Commit changes"
            echo -e "${ECHO_YELLOW}git status${ECHO_RESET}                    - Check status"
            echo -e "${ECHO_YELLOW}git pull${ECHO_RESET}                      - Pull changes from remote"
            echo -e "${ECHO_YELLOW}git push${ECHO_RESET}                      - Push changes to remote"
            echo -e "${ECHO_YELLOW}git branch${ECHO_RESET}                    - List local branches"
            echo -e "${ECHO_YELLOW}git checkout [branch]${ECHO_RESET}         - Switch branches"
            ;;
        bash)
            echo -e "${ECHO_BOLD_GREEN}Bash Cheatsheet:${ECHO_RESET}"
            echo -e "${ECHO_YELLOW}Ctrl+A${ECHO_RESET}                      - Move to beginning of line"
            echo -e "${ECHO_YELLOW}Ctrl+E${ECHO_RESET}                      - Move to end of line"
            echo -e "${ECHO_YELLOW}Ctrl+R${ECHO_RESET}                      - Search command history"
            echo -e "${ECHO_YELLOW}Ctrl+L${ECHO_RESET}                      - Clear screen"
            echo -e "${ECHO_YELLOW}Ctrl+U${ECHO_RESET}                      - Cut line before cursor"
            echo -e "${ECHO_YELLOW}Ctrl+K${ECHO_RESET}                      - Cut line after cursor"
            echo -e "${ECHO_YELLOW}Ctrl+Y${ECHO_RESET}                      - Paste cut text (yank)"
            ;;
        vim)
            echo -e "${ECHO_BOLD_GREEN}Vim Cheatsheet:${ECHO_RESET}"
            echo -e "${ECHO_YELLOW}i${ECHO_RESET}                         - Enter Insert mode"
            echo -e "${ECHO_YELLOW}Esc${ECHO_RESET}                       - Return to Normal mode"
            echo -e "${ECHO_YELLOW}:wq${ECHO_RESET}                       - Save and quit (:x)"
            echo -e "${ECHO_YELLOW}:q!${ECHO_RESET}                       - Quit without saving"
            echo -e "${ECHO_YELLOW}/[search]${ECHO_RESET}                  - Search forward for text"
            echo -e "${ECHO_YELLOW}dd${ECHO_RESET}                        - Delete current line"
            echo -e "${ECHO_YELLOW}yy${ECHO_RESET} / ${ECHO_YELLOW}p${ECHO_RESET}                   - Copy (yank) and Paste"
            echo -e "${ECHO_YELLOW}u${ECHO_RESET}                         - Undo last change"
            echo -e "${ECHO_YELLOW}Ctrl+R${ECHO_RESET}                      - Redo undone changes"
            ;;
        tmux)
            echo -e "${ECHO_BOLD_GREEN}Tmux Cheatsheet:${ECHO_RESET}"
            echo -e "${ECHO_YELLOW}tmux new -s [name]${ECHO_RESET}          - Create a new session"
            echo -e "${ECHO_YELLOW}tmux attach -t [name]${ECHO_RESET}       - Attach to existing session"
            echo -e "${ECHO_YELLOW}Ctrl+B, d${ECHO_RESET}                   - Detach from current session"
            echo -e "${ECHO_YELLOW}Ctrl+B, c${ECHO_RESET}                   - Create new window"
            echo -e "${ECHO_YELLOW}Ctrl+B, %${ECHO_RESET}                   - Split pane vertically"
            echo -e "${ECHO_YELLOW}Ctrl+B, \"${ECHO_RESET}                    - Split pane horizontally"
            echo -e "${ECHO_YELLOW}Ctrl+B, o${ECHO_RESET}                   - Switch to next pane"
            echo -e "${ECHO_YELLOW}Ctrl+B, w${ECHO_RESET}                   - List windows"
            ;;
        aliases)
            echo -e "${ECHO_BOLD_GREEN}Aliases Tools Cheatsheet:${ECHO_RESET}"
            echo -e "${ECHO_YELLOW}infra${ECHO_RESET}                     - cd to ~/git/ansible/infra_vars"
            echo -e "${ECHO_YELLOW}ff [name]${ECHO_RESET}                 - Find files by name (case-insensitive)"
            echo -e "${ECHO_YELLOW}fd [name]${ECHO_RESET}                 - Find directories by name (case-insensitive)"
            echo -e "${ECHO_YELLOW}da${ECHO_RESET}                        - Print current date/time string"
            ;;
        functions)
            echo -e "${ECHO_BOLD_GREEN}Functions Tools Cheatsheet:${ECHO_RESET}"
            echo -e "${ECHO_YELLOW}revert [branch]${ECHO_RESET}           - Git reset hard to branch/commit"
            echo -e "${ECHO_YELLOW}extract [file]${ECHO_RESET}            - Auto-extract archives (tar, zip, etc.)"
            echo -e "${ECHO_YELLOW}up [n]${ECHO_RESET}                    - Go up 'n' directories"
            echo -e "${ECHO_YELLOW}grept [string]${ECHO_RESET}            - Recursive grep with less pager"
            ;;
        *)
            echo -e "${ECHO_RED}No cheatsheet available for $command${ECHO_RESET}"
            echo -e "Try: ${ECHO_BOLD_YELLOW}cheatsheet git|bash|vim|tmux|aliases|functions${ECHO_RESET}"
            ;;
    esac
}

###################################################################
# 4. ENVIRONMENT
###################################################################
PATH=$PATH:$HOME/.local/bin:$HOME/bin
export PATH
export EDITOR='vim'
export VISUAL='vim'

export CLICOLOR=1
export LS_COLORS='no=00:fi=00:di=00;34:ln=01;36:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.gz=01;31:*.bz2=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.jpg=01;35:*.jpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.avi=01;35:*.fli=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.ogg=01;35:*.mp3=01;35:*.wav=01;35:*.xml=00;31:'

# Color for manpages in less makes manpages a little easier to read
export LESS_TERMCAP_mb=$'\E[01;31m'
export LESS_TERMCAP_md=$'\E[01;31m'
export LESS_TERMCAP_me=$'\E[0m'
export LESS_TERMCAP_se=$'\E[0m'
export LESS_TERMCAP_so=$'\E[01;44;33m'
export LESS_TERMCAP_ue=$'\E[0m'
export LESS_TERMCAP_us=$'\E[01;32m'

# set up XDG folders
export XDG_DATA_HOME="$HOME/.local/share"
export XDG_CONFIG_HOME="$HOME/.config"
export XDG_STATE_HOME="$HOME/.local/state"
export XDG_CACHE_HOME="$HOME/.cache"

###################################################################
# 5. HISTORY
###################################################################
# Source - https://stackoverflow.com/a
# Posted by fotinakis, modified by community. See post 'Timeline' for change history
# Retrieved 2025-12-29, License - CC BY-SA 4.0

# Eternal bash history.
# ---------------------
# Undocumented feature which sets the size to "unlimited".
# http://stackoverflow.com/questions/9457233/unlimited-bash-history
export HISTFILESIZE=
export HISTSIZE=
export HISTTIMEFORMAT="[%F %T] "
export HISTCONTROL=erasedups:ignoredups:ignorespace
# Ignore duplicates in history and some common commands
export HISTIGNORE="&:ls:ll:la:cd:exit:clear:history"
# Change the file location because certain bash sessions truncate .bash_history file upon close.
# http://superuser.com/questions/575479/bash-history-truncated-to-500-lines-on-each-login
export HISTFILE=~/.config/bash/bash_eternal_history
# Force prompt to write history after every command.
# http://superuser.com/questions/20900/bash-history-loss
PROMPT_COMMAND="history -a; $PROMPT_COMMAND"

###################################################################
# PROMPT
###################################################################
. ~/.config/bash/git-prompt.sh
PROMPT_COMMAND='PS1_CMD1=$(__git_ps1 " (%s)")'; PS1='\[\e[38;5;46;1m\]\u\[\e[0m\]@\[\e[38;5;252;1m\]\h\[\e[0m\]: \[\e[92;1m\]\w\[\e[38;5;51m\]${PS1_CMD1}\n\[\e[0m\]\$ '
