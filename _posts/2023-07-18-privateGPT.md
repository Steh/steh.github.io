---
title: "privateGPT"
categories: 
  - informationsecurity
tags:
  - blue team
classes: 
  - wide
excerpt: "PrivateGPT is a powerful AI project designed for privacy-conscious users, enabling you to interact with your documents using Large Language Models (LLMs) without the need for an internet connection."
toc: true
date: 2023-07-18
---

## Installation

```bash
# clone Repo
git clone https://github.com/imartinez/privateGPT.git

# enter Repo
cd privateGPT

# virtuelle Umgebung erstellen
python3 -m privateGPT venv

# umgebung betretten
source privateGPT/bin/active

# Requirements installieren
pip3 install -r requirements.txt

# download model
mkdir models
cd models
curl -O https://gpt4all.io/models/ggml-gpt4all-j-v1.3-groovy.bin

# config 
cp example.env .env

# read documents
python3 ingest.py

# start gpt
python3 privateGPT.py
```

## source

* [github: privateGPT][def]
* [Training Your Own LLM using privateGPT][def1]

[def]: https://github.com/imartinez/privateGPT
[def1]: https://levelup.gitconnected.com/training-your-own-llm-using-privategpt-f36f0c4f01ec
