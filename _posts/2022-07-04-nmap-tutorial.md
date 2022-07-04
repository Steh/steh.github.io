---
layout: post
title: "nmap cheat sheet"
categories: [nmap, cheatsheet]
tags: ['cheatsheet', 'nmap']
autor: StehSa
--- 

# nmap: Cheat Sheet
	nmap -sC -sV xx.xx.xx.xx

	-sC: Performs a script scan using the default set of scripts. It is equivalent to --
	script=default. Some of the scripts in this category are considered intrusive and
	should not be run against a target network without permission.
	-sV: Enables version detection, which will detect what versions are running on what port.
	

[Kali.org: nmap Usage Example](https://www.kali.org/tools/nmap/)
[linux.die.net: nmap(1) - Linux man page](https://linux.die.net/man/1/nmap)
