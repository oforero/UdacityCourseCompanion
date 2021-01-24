https://medium.com/udacity-course-companion/extend-the-zsh-prompt-with-git-information-b953305bf066
Extend the ZSH Prompt with GIT information
==========================================

[![Oscar Mauricio Forero Carrillo](https://miro.medium.com/fit/c/96/96/1*RbLyPocQjcSragh4GPhpVA.jpeg)](https://oforero.medium.com/?source=post_page-----b953305bf066--------------------------------)[Oscar Mauricio Forero Carrillo](https://oforero.medium.com/?source=post_page-----b953305bf066--------------------------------)Follow[Dec 29, 2020](https://medium.com/udacity-course-companion/extend-the-zsh-prompt-with-git-information-b953305bf066?source=post_page-----b953305bf066--------------------------------) · 5 min read

<img alt="Image for post" class="t u v gs aj" src="/_images/bmc_button.png" width="3000" height="3000" srcSet="https://miro.medium.com/max/552/1\*xBwkF0k0o\_hMUOBEOnbNCw.png 276w, https://miro.medium.com/max/1104/1\*xBwkF0k0o\_hMUOBEOnbNCw.png 552w, https://miro.medium.com/max/1280/1\*xBwkF0k0o\_hMUOBEOnbNCw.png 640w, https://miro.medium.com/max/1400/1\*xBwkF0k0o\_hMUOBEOnbNCw.png 700w" sizes="700px"/>


![BMC Button](/assets/imgs/bmc_button.png)
[bmc](https://www.buymeacoffee.com/oforero)

I am an Udacity mentor, and I helped many students move forward with their GitHub project.

Apple switched the default command-line shell to _ZSH_. This is the cause of the most common issue faced by students using Apple computers for this course.

Introduction
============

The shell is the program through which humans interact with the computer. Graphical user interfaces are popular, but text-based shells are still essential for developers.

Udacity’s includes instructions about how to customize the command line. These customizations ease the _GIT_ workflow by reducing the need to use `git status` or `git branch`.

In \*nix Operating Systems there are many command-line shells to chose from. _BASH_ is the most popular, but it is no longer the default shell for _macOS_.

We have four options to deal with the problems caused by Apple’s decision.

Option 1: Manually start _BASH_
===============================

This is the simpler option. We can start _BASH_ by typing bash — login in the terminal.

BASH reads the `.bash_profile`only when it starts as login shell. Hence we need to pass the `--login` parameter to load the configuration.

<img alt="Image for post" class="t u v gs aj" src="https://miro.medium.com/max/3156/1\*W9MoSdNFf90mv2hBpCyAqg.gif" width="1578" height="1056" srcSet="https://miro.medium.com/max/552/1\*W9MoSdNFf90mv2hBpCyAqg.gif 276w, https://miro.medium.com/max/1104/1\*W9MoSdNFf90mv2hBpCyAqg.gif 552w, https://miro.medium.com/max/1280/1\*W9MoSdNFf90mv2hBpCyAqg.gif 640w, https://miro.medium.com/max/1400/1\*W9MoSdNFf90mv2hBpCyAqg.gif 700w" sizes="700px"/>

We can go back to the previous shell by typing exit.

Option 2: Make BASH the default shell
=====================================

The shell in \*nix system is customisable per user; we can change our default back to _BASH_.

<img alt="Image for post" class="t u v gs aj" src="https://miro.medium.com/max/3156/1\*jpy\_kmhFmgdTdRjFJLbP\_w.gif" width="1578" height="1056" srcSet="https://miro.medium.com/max/552/1\*jpy\_kmhFmgdTdRjFJLbP\_w.gif 276w, https://miro.medium.com/max/1104/1\*jpy\_kmhFmgdTdRjFJLbP\_w.gif 552w, https://miro.medium.com/max/1280/1\*jpy\_kmhFmgdTdRjFJLbP\_w.gif 640w, https://miro.medium.com/max/1400/1\*jpy\_kmhFmgdTdRjFJLbP\_w.gif 700w" sizes="700px"/>

Note that changing the default login shell won’t change the currently running shell. We need to start a new window or tab to see the effect.

I do not recommend this option, because newer tutorials and tools will assume _ZSH_ is the shell on Macs. Yet, changing it is not difficult,, and we can always change it back if it creates any issues.

Options 3: Configure ZSH using the git-prompt.sh script
=======================================================

The final option and best option is to configure _ZSH_ to show the _GIT_ information as we did for _BASH_.

_ZSH_ has many configuration options. And it has frameworks that allow us to control the look and feel of the command line to extents one wouldn’t suspect. The most popular ones are [_oh-my-zsh_](https://github.com/ohmyzsh/ohmyzsh) and [_prezto_](https://github.com/sorin-ionescu/prezto)_._

On this tutorial we will keep it simple and do exactly the same configuration that we did for _BASH_.

In ZSH the default configuration file is `.zshrc`.

ZSH has its own autocomplete framework compatible with GIT, to activate it we need to add the following line to the resource file:

```
autoload -Uz compinit && compinit
```

When running for the first time it is possible that we get a security warning:

```
zsh compinit: insecure directories, run compaudit for list.  
Ignore insecure directories and continue \[y\] or abort compinit \[n\]?
```

This means files are being loaded from directories with more permissive permissions than necessary.

To solve it we execute compaudit and change the permissions for all the folders listed.

```
compaudit | xargs chmod 744
```

ZSH has also a framework to get information from version control systems, but we would like to configure it as similar to BASH as possible.

The `git-prompt.sh` script included with GIT and downloadable from Udacity’s resource page is compatible with ZSH.

This means we can use the same configuration as with BASH, but in the `.zshrc` file:

```
source ~/.git-prompt.shsetopt PROMPT\_SUBST ; PS1='\[%n@%m %c$(\_\_git\_ps1 " (%s)")\]\\$ '
```

This will show the branch in the prompt but without any colors.

<img alt="Image for post" class="t u v gs aj" src="https://miro.medium.com/max/3168/1\*VEbhVZ1fmQpCdP4TMOBjUQ.png" width="1584" height="428" srcSet="https://miro.medium.com/max/552/1\*VEbhVZ1fmQpCdP4TMOBjUQ.png 276w, https://miro.medium.com/max/1104/1\*VEbhVZ1fmQpCdP4TMOBjUQ.png 552w, https://miro.medium.com/max/1280/1\*VEbhVZ1fmQpCdP4TMOBjUQ.png 640w, https://miro.medium.com/max/1400/1\*VEbhVZ1fmQpCdP4TMOBjUQ.png 700w" sizes="700px"/>

Options 4: Configure ZSH using ZSH tools only
=============================================

As we discussed before, ZSH has extensive configuration options, but for this article we will keep it simple and do a minimal configuration without using any frameworks.

We start by activating autocomplete, exactly as we did before.

```
autoload -Uz compinit && compinit
```

Then we use the tool included with ZSH to communicate with source control systems:

```
setopt prompt\_subst  
autoload -Uz vcs\_info  
zstyle ':vcs\_info:\*' stagedstr 'S'   
zstyle ':vcs\_info:\*' unstagedstr 'U'   
zstyle ':vcs\_info:\*' check-for-changes true  
zstyle ':vcs\_info:\*' actionformats '%F{5}\[%F{2}%b%F{3}|%F{1}%a%F{5}\]%f '  
zstyle ':vcs\_info:\*' formats \\  
  '%F{5}\[%F{2}%b%F{5}\] %F{2}%c%F{3}%u%f'  
zstyle ':vcs\_info:git\*+set-message:\*' hooks git-untracked  
zstyle ':vcs\_info:\*' enable git   
+vi-git-untracked() {  
  if \[\[ $(git rev-parse --is-inside-work-tree 2> /dev/null) == 'true' \]\] && \\  
  \[\[ $(git ls-files --other --directory --exclude-standard | sed q | wc -l | tr -d ' ') == 1 \]\] ; then  
  hook\_com\[unstaged\]+='%F{1}?%f'  
fi  
}  


precmd () { vcs\_info }  
PROMPT='%F{5}\[%F{2}%n%F{5}\] %F{3}%3~ ${vcs\_info\_msg\_0\_} %f%# '
```

This will show a prompt with the following format:

```
\[user\] FQN folder \[branch\] \[Status Info\] %
```

The status info shows a yellow M for unstaged changes, a green M for staged changes, and a question mark `?` for untracked files.

<img alt="Image for post" class="t u v gs aj" src="https://miro.medium.com/max/3156/1\*OIxZ02w5CRpyVMazmXdg3A.gif" width="1578" height="1056" srcSet="https://miro.medium.com/max/552/1\*OIxZ02w5CRpyVMazmXdg3A.gif 276w, https://miro.medium.com/max/1104/1\*OIxZ02w5CRpyVMazmXdg3A.gif 552w, https://miro.medium.com/max/1280/1\*OIxZ02w5CRpyVMazmXdg3A.gif 640w, https://miro.medium.com/max/1400/1\*OIxZ02w5CRpyVMazmXdg3A.gif 700w" sizes="700px"/>

Conclusion
==========

We have explored different options to configure the shell on _macOS_ to work with _GIT_. This options would allow us to follow the instructions from Udacity’s course in the versions of _macOS_ that do not longer use _BASH_ as default shell.

Now, go back and learn!

If you enjoyed the article and found it useful, please consider buying me a coffee.

[

<img alt="Image for post" class="t u v gs aj" src="https://miro.medium.com/max/340/1\*Dpw8-hNGI2fDmosV4E8DVQ.png" width="170" height="37"/>

](https://www.buymeacoffee.com/oforero)
