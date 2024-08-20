## Reset Jetbrains trials

To reset Pycharm or other Jetbrains products, create a shell script containg
the following lines
```
#!/bin/sh
rm -rf ~/.java/.userPrefs/prefs.xml
rm -rf ~/.java/.userPrefs/jetbrains/prefs.xml
rm -rf ~/.java/.userPrefs/jetbrains/pycharm
rm -rf ~/.config/JetBrains/PyCharm*/eval
rm -rf ~/.config/JetBrains/PyCharm*/options/other.xml
```
Let's say the file name is [reset_pycharm.sh](reset_pycharm.sh). If you are 
using other products other than Pycharm, i.e. Webstorm, Phpstorm etc, then 
replace that with the name provided in line 5 & 6.

Now, make the script executable. 
```
sudo chmod +x reset_pycharm.sh
```
Now, you can run the script to reset your trail version of Pycharm
```
./reset_pycharm.sh
```

There are some other methods too(not tested), you can test them also.

**Alternate Method 1**
```
#!/bin/bash

#rm -rf ~/.java/.userPrefs/prefs.xml
#rm -rf ~/.java/.userPrefs/jetbrains/prefs.xml

# Reset PyCharm
rm -rf ~/.config/JetBrains/PyCharm*/eval
# rm -rf ~/.config/JetBrains/PyCharm*/options/other.xml
sed -i -E 's/<property name=\"evl.*\".*\/>//' ~/.config/JetBrains/PyCharm*/options/other.xml
rm -rf ~/.java/.userPrefs/jetbrains/pycharm

# Reset IntelliJ IDEA
rm -rf ~/.config/JetBrains/IntelliJIdea*/eval
# rm -rf ~/.config/JetBrains/IntelliJIdea*/options/other.xml
sed -i -E 's/<property name=\"evl.*\".*\/>//' ~/.config/JetBrains/IntelliJIdea*/options/other.xml
rm -rf ~/.java/.userPrefs/jetbrains/idea

# Reset WebStorm
rm -rf ~/.config/JetBrains/WebStorm*/eval
# rm -rf ~/.config/JetBrains/WebStorm*/options/other.xml
sed -i -E 's/<property name=\"evl.*\".*\/>//' ~/.config/JetBrains/WebStorm*/options/other.xml
rm -rf ~/.java/.userPrefs/jetbrains/webstorm
```
**Alternate Method 2**
```
cd ~/.IntelliJIdea[YOUR_VERSION]/
rm config/eval/idea[YOUR_VERSION].evaluation.key
rm config/options/other.xml
cd ~/.java/.userPrefs/jetbrains/
rm -Rf idea/
```