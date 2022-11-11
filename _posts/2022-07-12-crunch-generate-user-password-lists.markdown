---
layout: post
title:  "crunch: generate user/password lists"
date:   2022-07-11
categories: crunch kali
---

    # create wordlists
    ## 1 5          = Character count between 1 and 5
    ## rstuvwxyz    = all included characters
    ## -o           = outputfile
    crunch 1 5 rstuvwxyz -o /root/users.txt

    ## basic command
    crunch <min. password length> <max. password length> <character space> -o <saving_location>


* [Kali: crunch](https://www.kali.org/tools/crunch/)