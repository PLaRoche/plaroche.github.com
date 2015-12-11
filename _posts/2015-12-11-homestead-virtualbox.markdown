---
layout: post
title:  "Homestead and web timeouts: Damn you vboxnet0"
date:   2015-12-11
---

Not able to load your web project, is the browser just timing out?  


Chances are your Homestead.yaml file has a different IP range as what __VirtualBox__ has set up.



#### Example:  

Some config:

- My homestead.yaml file (`~/.homestead/Homestead.yaml`) file has `10.1.10.1` as its IP
- My `/etc/hosts` file has `10.1.10.1 myapp.app` in it

After `homestead up` :

- I try `telnet myapp.app 80` from my laptop to my vm... nothing.....
- Yet `telnet localhost 8000` works (homestead sets that forward up for me).... hmmm

Check out VirtualBox:

- In VirutalBox: Open virtualbox's preferences (not for your vm, for vbox itself) -> Network -> Host Only
- Double click on vboxnet0 (if you have more then one, you will need to go to the network prefs of your vm and see which one it is using)
- Set its ip range __to the same range__ as the one your Homestead.yaml file has.  In my example `10.1.10.2` would work (note: don't use the same IP, you will have a conflict)
- You can select DCHP Server and just turn it off (or make its IP stuff correct)
- *Alternatively* You could have made your Homestead.yaml file match the virtual network

End result:

In my browser, I can now `http://myapp.app` and see my app!





