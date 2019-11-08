---
layout: post
title: "My personal clean-install script"
subtitle: "This is a subtitle"
date: 2019-11-05 23:10:00 -0400
background: '/backgrounds/04.png'
---

I take pride in the fact that I've kept my macbook of 6 years running in near perfect condition. Every once in a
while
I'll do a clean install to get everything back to a clean working state. But sometimes getting my laptop
back to the state I had it in tends to take a lot of time and effort which is why I've decided to automate as much
of it
as I can. Cutting down work you need to do into something that takes about 15 minutes is what we're all here for,
isn't
it?

The script basically takes in your home directory as input and then based off a list of files it creates a symbolic
link
between the dotfiles backed up in my git repo and my actual dotfiles. Now my zshrc and vimrc profiles are populated
with
my specifications and customizations.
Next it will run the brew script which simply uses brew and brew-cask to install a list of my most important
applications. Among them are zsh, python, postgres, and all my regular applications like spotify

The most important step for me personally because I always forget how to do this and have to spend a significant
amount
of time looking it up again is my terminal customizations. Zsh and zsh completions have already been installed by
the
brew script so what's left is for us to change the default shell from bash to zsh. We finish up by installing
oh-my-zsh
and downloading my favorite iterm2 theme from github.

The last thing I like to do is related to my python setup. I have a text file with my essential python libraries
such as
jupyter and virtualenvwrapper, things I use all the time. I pip install those.


I'd like to add a script to systematically backup my most important directories and maybe also unpack them back into
their correct places. That way I will have to do very little the next time I run a clean install or migrate to a new
laptop.


{% highlight bash %}
# change shell to zsh
echo "changing shell from bash to zsh "
SHELL=/usr/local/bin/   # brew version of zsh
echo $SHELL | sudo tee -a /etc/shells
chsh -s $(which zsh)
source ~/.zshrc
{% endhighlight %}