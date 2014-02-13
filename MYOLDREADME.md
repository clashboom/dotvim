TODO: Rewrite this thing

First things first
=====================

#### Derek Wyatt ####
@derekwyatt
http://derekwyatt.org/

This guy is the sole reason I started using Vim.
Awesome Vim tutorials can be found on his site.
Thank you, Derek!

#### Shougo ####
@Shougo

His plugins make up the core of my current config. Great stuff.

#### Tim Pope ####
@tpope

Essential plugins for any vim config.
Especially for rubyists.

#### Juan Pedro Fisanotti ###
@fisadev

Initially his config was more or less what I used.
It's great. Lots of python stuff that still remain in my config.
Check it out.

#### Vim community ####
Thank you! For plugins and stuff. For everything.

Now, on to the install and configuration.

#Installing VIM on debian based distros
My distro of choice: Crunchbang #!, but should work on any debian based distro

https://github.com/Valloric/YouCompleteMe/wiki/Building-Vim-from-source

$ sudo apt-get install git mercurial

$ sudo apt-get remove vim vim-runtime gvim vim-tiny vim-common vim-gui-common

$ sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev
libgtk2.0-dev libatk1.0-dev libbonoboui2-dev
libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev ruby-dev
libperl-dev liblua5.1-dev lua5.1 libluajit-5.1

If necessary, install luajit manually. If needed, run
$ ldconfig
If lua links are not sane when configuring vim, run
$ sudo ln -s /usr/lib/liblua5.1.so /usr/local/lib/liblua.so
If running into problems see the log file (src/auto/config.log)

Why is Lua needed? Because its a dependency for Shougo's awesome plugins.
So make sure you get it. Lua as well as luajit.

$ cd ~
$ hg clone https://code.google.com/p/vim/
$ cd vim
$ ./configure --with-features=huge
            --enable-rubyinterp
            --enable-pythoninterp
            --enable-perlinterp
            --enable-cscope
            --enable-luainterp
            --with-luajit
$ make
$ sudo make install

$ sudo apt-get install exuberant-ctags python-pip build-essential
$ sudo pip install --upgrade pip
$ sudo pip install dbgp vim-debug pep8 flake8 pyflakes

Set vim as your default editor with update-alternatives.
$ sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1
$ sudo update-alternatives --set editor /usr/bin/vim
$ sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1
$ sudo update-alternatives --set vi /usr/bin/vim

Setup NeoBundle
$ mkdir -p ~/.vim/bundle
$ git clone git://github.com/Shougo/neobundle.vim ~/.vim/bundle/neobundle.vim

Install powerline symbols
"https://powerline.readthedocs.org/en/latest/installation/linux.html"

Create symlinks, if you place your config file somewhere else:
$ ln -s ~/.vim/vimrc ~/.vimrc
$ ln -s ~/.vim/gvimrc ~/.gvimrc

After adding fancy fonts, reset font cache:
$ xset fp rehash or fc-cache -fv

Really nice tutorial for learning all the essential vim shortcuts
before diving into plugin stuff.
http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html


# Installing Virtualenv and virtualenvwrapper
http://calvinx.com/2013/07/11/python-virtualenv-with-node-environment-via-nodeenv/

$ sudo pip install --upgrade virtualenv
$ sudo pip install virtualenvwrapper

Add this stuff to your .bashrc
export WORKON_HOME=~/envs
mkdir -p $WORKON_HOME
source /usr/local/bin/virtualenvwrapper.sh

If you are having some install glitch and getting error messages when starting bash, try:

wget http://python-distribute.org/distribute_setup.py
sudo python distribute_setup.py


$ mkvirtualenv myproject1 # Make a project directory

# Adding Node environment
 This installs the nodeenv package into our new python virtualenv so named "myproject1" above
$ pip install nodeenv
This commands installs nodejs and adds new shell functions to our virtualenvwrapper shell functions
$ nodeenv -p
* Install node.js (0.10.12) ..
* Appending nodeenv settings to /Users/calvin/.virtualenvs/myproject1/bin/activate
Deactivate and re-activate to ensure we load in the updated shell functions and environment
$ deactivate; workon project1

Useful virtualenvwrapper commands
You can see installed packages with lssitepackages
postmkvirtualenv is run when a new environment is created, letting you automatically install commonly-used tools.

Install what you need
$ npm install -g yo grunt-cli bower
$ npm install -g generator-webapp


# Adding Google Appengine
Download appengine, pop it in your project folder
$ unzip ~/Downloads/google_appengine_1.7.7.zip
$ mv google_appengine google_appengine_1.7.7
$ ln -s google_appengine_1.7.7 gae

Edit bin/activate to look like this:
PATH="$VIRTUAL_ENV/bin:$PATH"
PATH="$VIRTUAL_ENV/gae:$PATH"   # New line for GAE
export PATH

Add gae.pth:
$cat lib/python2.7/site-packages/gae.pth
../../../../gae  # <-- relative path to gae directory
import dev_appserver; dev_appserver.fix_sys_path()

Scaffold your app and you are ready to go
$ yo angular


# Miscellany (Stylus, Jade, etc)
pip install PIL in virtualenv for python-images (make sure you have python-dev
installed on your machine)

Stylus:
https://github.com/yeoman/yeoman/wiki/Stylus-integration
npm install grunt-contrib-stylus --save-dev

Jade
npm install grunt-contrib-jade --save-dev

# Crunchbang config
To change resolution in your ~/.config/openbox/autostart add:
xrandr --output default --mode 1920x1080 &
For dual monitor setup:
xrandr --auto --output VGA-0 --mode 1920x1080 --left-of DVI-0

Keyboard layouts in /usr/share/X11/xkb/symbols and check the specific one for variants
Add to openbox autostart
setxkbmap -option grp:switch,grp:shifts_toggle,grp_led:scroll us,lv,no,ru -variant ,apostrophe,, &
(sleep 5s && fbxkb) &
Reboot or restart X to reload changes
sudo pkill X

Add top and network bandwidth to concky
$processes processes ($running_processes running)

NAME $alignr PIDCPU
${top name 1} $alignr ${top pid 1} ${top cpu 1}
${top name 2} $alignr ${top pid 2} ${top cpu 2}
${top name 3} $alignr ${top pid 3} ${top cpu 3}
${top name 4} $alignr ${top pid 4} ${top cpu 4}
${top name 5} $alignr ${top pid 5} ${top cpu 5}
${top name 6} $alignr ${top pid 6} ${top cpu 6}
${top name 7} $alignr ${top pid 7} ${top cpu 7}
${top name 8} $alignr ${top pid 8} ${top cpu 8}
${top name 9} $alignr ${top pid 8} ${top cpu 9}

Inbound $alignr ${downspeed eth0} kb/s
${downspeedgraph eth0}
Outbound $alignr ${upspeed eth0} kb/s
${upspeedgraph eth0}

Get a sensible bash prompt
https://github.com/paulirish/dotfiles/blob/master/.bash_prompt

Useful utilities:
$ sudo apt-get install tree speedcrunch xclip

Some monitoring tools:
$ sudo apt-get iostat lsof sar

Entertainment and misc:
$ sudo apt-get install artha mpd mpc ncmpcpp zathura
Guide for mpd - http://crunchbang.org/forums/viewtopic.php?pid=182574

Get additional sources.list for crunchbang
https://sites.google.com/site/mydebiansourceslist/




