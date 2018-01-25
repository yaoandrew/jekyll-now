---
layout:  post
title: Tools of the Trade - My Current Dev Environment
tags: ["tools", "developer", "environment"]
---
![VIM xkcd cartoon](https://imgs.xkcd.com/comics/real_programmers.png)


Everyone knows to be wary of discussing politics or religion when meeting someone new or during the family get together at Thanksgiving. Similarly in software engineering, the topics guaranteed to involve passionate differences in opinion are around the setup and tools which we use for our craft. The choices of which editor, tabs vs. spaces, which window manager, and which shell have be known to both end in rightgeous indignation and [torpedo promising fictional relationships](https://www.youtube.com/watch?v=SsoOG6ZeyUI).

When I started my first real job, I worked at an investment bank that had an industry pioneering electronic trading system. With a push of a button, we could trade a basket of hundreds of stocks in seconds. This was still an obscure corner of the trading floor as most of the Street could be seen talking on two phone handsets and furiously scribbling on paper tickets with bad handwriting. These tickets made actual carbon copies (cc:) in three different colors of the barely ledgible writing.

As the new, low man on the totem pole, I was offered a folding chair and the oldest and probably slowest machine they could scrape together, the Sun Sparcstation 5. I still remember looking around at my coworker Andrew's machine and noticing two important distinctions - he had a Sparc 20 and had customized his desktop with multi-time zone clocks, CPU and memory graphs, and Xeyes which followed around your mouse movements. As I sat there feeling like my work wasn't worthy of a higher spec machine (*spoiler: it wasn't*), I also faced the indignity of using the generic default desktop. I vowed to scour every man page on my machine and get root access from our militant sysadmin so I could look more legit. In the process, I learned a bit about shells, dotfiles, and window managers which I still use today to configure my dev environment.

My most recent setup could still use some improvement but I've mostly abstracted away the hardware. My goal was to be able to sit down at any machine and quickly get my dev environment up and running. This first round was mostly about making my setup files accesible and I'll probably try to automate a lot of the dependency installation down the road.

The basics (OS)
I'm usually on the latest release of MacOS (currently 10.12.6)

Xcode

iTerm2
 font 14pt Input Mono Condensed Extra Light
 General | Selection | Applications in terminal may access clipboard
 tmux integration | Open tmux windows as native windows

Package Management
 Homebrew
 packages
 language support - elixir, erlang, ruby, python
 tools - git, irssi, nmap, openssl, shiftit, tmux, tree, z

Shell
 zsh, oh-my-zsh

vimrc

vim plugin management

.tmux.conf

tmux plug in management
TPM

