# How Easy It Is To Switch To Zsh

With the latest MacOS release, Catalina, the default operating shell was switched from `bash` to 
`zsh`. This was announced pretty early on, so it wasn't a surprise and I had "Learn ZSH" on my to 
do listfor quite some time but now that I have updated my machines, it reminds you that you need 
to switch to zsh. And while it is possible to hide that message, this is as good opportunity as 
ever to make the switch.

There are several frameworks that make it easy to switch as well. The most popular of them is
Robby Russell's Oh My Zsh. It seems easy to install and but at first glance, it doesn't have the 
customization and control I want. I instead chose to try Antigen first. It is similar to a Vim
framework called Vundle in philosphy and even allows you to build off OMZ. Antigen is a package
manager for `zsh` and keeps its plugins in what it calls "bundles". 

Setting up Antigen took less than 10 minutes. I first installed all of the requirements:
```
$ brew install zsh
$ brew install antigen
```

and then I copied the the `.zshrc` example from the website:

```
source $(brew --prefix)/share/antigen/antigen.zsh
antigen use oh-my-zsh

antigen bundle git

# Syntax highlighting bundle.
antigen bundle zsh-users/zsh-syntax-highlighting

# Fish-like auto suggestions
antigen bundle zsh-users/zsh-autosuggestions

# Extra zsh completions
antigen bundle zsh-users/zsh-completions

# Load the theme
antigen theme robbyrussell

antigen apply
```

This does several things. The first two lines start antigen and set it up with a default set of
configurations. Then, I add several bundles to add functionality to the shell. These often come in
the form of auto-completion or set up commands that are typically in a `.bash_profile` or `.bashrc`
file. Lastly, I chose a built-in theme and told `antigen` to apply those changes. When a session is
started, it will install those bundles and themes, if they are not already installed, and then sets
up the sesson.

Now you can just start a `zsh` session by running

```
$ zsh
```

This won't switch your shell permanently, it just starts a new session over your current session. This
is nice because it allows you to add or remove things to your `.zshrc` file before entering entering 
the command that Apple gives to switch your shell over permanently. 

That is just a basic zsh configuration. The next step is to move over the rest of my current 
bash shell functionality. My current set up is not too complex, so there are probably plugins or 
themes that have what I want out of the box.
