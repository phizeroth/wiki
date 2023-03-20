---
title: color bash prompt
description: 
published: true
date: 2023-03-20T20:43:26.878Z
tags: 
editor: markdown
dateCreated: 2023-03-20T20:43:26.878Z
---

# .bashrc

Replace/modify the default color block in the `.bashrc` with this for a more intuitive experience customizing the bash colors:
```bash
# ----------------------
# CONFIGURE COLOR PROMPT
# Replace default color prompt if-block
config_color_prompt () {
    if [ "$color_prompt" = yes ]; then

        local GREEN='\e[32m'
        local CYAN='\e[96m'
        local ORNG='\e[38;5;202m'

        local BOLD='\e[1m'
        local PLAIN='\e[0m'
        local RESET='\[$(tput sgr0)\]'

        local USR=${BOLD}${GREEN}
        local AT=${BOLD}${CYAN}
        local HOST=${BOLD}${ORNG}
        local PATH=${PLAIN}${CYAN}
        local CURSOR=${BOLD}${ORNG}

        PS1="${debian_chroot:+($debian_chroot)}${USR}\u${AT}@${HOST}\h${PATH} \w ${CURSOR}\$${RESET} "
#        PS1='${debian_chroot:+($debian_chroot)}\[\e[01;32m\]\u\[\e[96m\]@\[\e[01;95m\]\h\[\e[96m\] \w \[\e[01;95m\]\$\$    else
        PS1="${debian_chroot:+($debian_chroot)}\u@\h:\w\$ "
    fi
}
config_color_prompt
# ----------------------
```
# Handy scripts

## `16-color.sh`
```bash
    #!/bin/bash

    for clfg in {30..37} {90..97} 39 ; do
            #Formatting
            for attr in 0 1 2 4 5 7 ; do
                    #Print the result
                    echo -en "\e[${attr};${clfg}m ^[${attr};${clfg}m \e[0m"
            done
            echo #Newline
    done

    exit 0
```

## `256-color.sh`
```bash
    #!/bin/bash

    for fgbg in 38 48 ; do # Foreground / Background
        for color in {0..255} ; do # Colors
            # Display the color
            printf "\e[${fgbg};5;%sm  %3s  \e[0m" $color $color
            # Display 6 colors per lines
            if [ $((($color + 1) % 6)) == 4 ] ; then
                echo # New line
            fi
        done
        echo # New line
    done

    exit 0
```

##  `colors_and_formatting.sh`
```bash
   #!/bin/bash

    #Background
    for clbg in {40..47} {100..107} 49 ; do
        #Foreground
        for clfg in {30..37} {90..97} 39 ; do
                #Formatting
                for attr in 0 1 2 4 5 7 ; do
                        #Print the result
                        echo -en "\e[${attr};${clbg};${clfg}m ^[${attr};${clbg};${clfg}m \e[0m"
                done
                echo #Newline
        done
    done

    exit 0
```

# References
* https://misc.flogisoft.com/bash/tip_colors_and_formatting
* https://bashrcgenerator.com/