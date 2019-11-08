---
layout: post
title: "MacOS Clean-install & Setup Script"
subtitle: "This is a subtitle"
date: 2019-11-05 23:10:00 -0400
background: '/backgrounds/09.png'
---

I take a lot of pride in the fact that I’ve kept my macbook of 6 years running in near perfect condition. Every once in a while, when installing a new OS or when I feel like my system is bloated and cluttered I'll do a clean install to bring things back to a good working state. This process, while not technically difficult, can be long and inconvenient which is why I've decided to to automate as much of it as I can. In the end if I can cut down something that takes about an hour to 15 minutes then that's what we're all here for isn't it? Plus, there's the added benefit of doing without looking up everything I've ever done to get my system back to it's formal glory. 

To start with, my script takes in a directory as input to setup the path to my dotfiles and then cd's into it to be able to run all my installation scripts. 

Next we install Homebrew (MacOS's best package manager) followed by the brew.sh script which systematically installs most if not all, my main packages. This script will install everything from my shell related packages such as zsh, zsh-completions, to my desktop applications using brew cask, to an assortment of random things like postgresql and tree (a recursive directory listing that’s easy on the eyes).

The most important step for me personally because I always forget how to do this and have to spend a significant amount of time looking up again and again is my terminal customizations. Since zsh has just been installed by brew, we need to let the terminal know to switch to it as our main shell. And that's exactly what we do here:

{% highlight bash %}
# change shell to zsh
echo "changing shell from bash to zsh "
SHELL=/usr/local/bin/   # brew version of zsh
echo $SHELL | sudo tee -a /etc/shells
chsh -s $(which zsh)
source ~/.zshrc
{% endhighlight %}


In my opinion, what makes zsh truly great is the wonderful framework oh-my-zsh, which adds a bunch of convenient and useful configurations and makes using zsh so fun. 

{% highlight bash %}
# install oh-my-zsh
echo "Installing oh-my-zsh ..."
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
{% endhighlight %}


The last important step is for me to be able to create symbolic links to my dotfiles so that I'm always able to back them up and have copies of my settings. 

{% highlight bash %}
# list of files/folders to symlink in ${homedir}
files="zshrc vimrc"
# create symlinks (will overwrite old dotfiles)
echo "Creating symbolic link for dotfiles"
for file in ${files}; do
   echo "Creating symlink to $file in home directory."
   ln -sf ${dotfiledir}/.${file} ${homedir}/.${file}
done
echo "...done"
{% endhighlight %}


If you'd like to checkout my scripts, you can find it [here](https://github.com/tmtaybah/dotfiles). 