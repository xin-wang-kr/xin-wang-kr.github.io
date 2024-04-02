---
title: Use Python-based PyCX simulator on MacOS M1
date: 2024-04-02
permalink: /posts/2024/04-Aster
excerpt_separator: <!--more-->
toc: true
tags:
  - aster
---
This instruction will show how to connect Aster server to Visual Studio Code.

__NOTE__: Please don’t forget to connect through VPN, if you need it.
**Step 1: Login to server through ssh in terminal.** 



**Step 2: Create a new Python notebook inside this directory.**

![image](https://user-images.githubusercontent.com/28020765/223584837-0dd11058-d113-43cc-82e9-a4a953dcf845.png)

**Step 3: Install PyQt6.**
```sh
!pip install PyQT6
```

<img width="853" alt="image" src="https://user-images.githubusercontent.com/28020765/223585034-e05b02a1-0074-447b-8f49-7b480d085eb1.png">

**Step 4: Find pycxsimulator.py file inside PyCX directory and add the codes at the top as below.**
```sh
import PyQt6.QtCore
import os
os.environ["QT_API"] = "pyqt5"
```

<img width="510" alt="image" src="https://user-images.githubusercontent.com/28020765/223585444-9f9b3646-5a66-48c0-b24d-59d1d79063be.png">

**Step 5: Launch any simulator.**
```sh
!python ca-panic.py
```

<img width="1072" alt="image" src="https://user-images.githubusercontent.com/28020765/223586394-686b1862-bf22-4882-beb8-957beb7750e9.png">



