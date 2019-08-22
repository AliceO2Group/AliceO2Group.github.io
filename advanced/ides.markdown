---
title: IDE support
layout: main
---

CLion
=====

Compilation
-----------

1. Build with aliBuild as you would do normally
2. Extract the environment variables and copy them \
  `alienv printenv QualityControl/latest | tr ";" "\n" | grep -v export | sed -e 's/[[:space:]]*$//' | grep -v unset` \
  On _Mac_ one can directly get the output in the clipboard: `alienv printenv QualityControl/latest | tr ";" "\n" | grep -v export | sed -e 's/[[:space:]]*$//' | grep -v unset | pbcopy`
3. In CLion got to the _settings_ or _preferences_ window
4. Access the cmake configuration (see number 1 on figure below)
5. Edit the environment variables (see number 2 on figure below)
6. Paste the clipboard content using the button labelled 3 in the figure

![alt text](../images/IDEconfig.png)

Editor
------

Coding guidelines can be applied by using a special settings file. See [here](https://github.com/AliceO2Group/CodingGuidelines#clion).