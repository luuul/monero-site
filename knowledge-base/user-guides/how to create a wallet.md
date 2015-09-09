---
layout: static_page
title: "Creating a Monero wallet"
title-pre-kick: "Creating a Monero wallet "
title-kick: "on Ubuntu "
title-post-kick: ""
kick-class: "purple-kicks"
icon: "icon_userguides"
attribution: "<!-- Icon is based on work by Freepik (http://www.freepik.com) and is licensed under Creative Commons BY 3.0 -->"
---

### Operating Systems:  Ubuntu

#### Resource for Monero Binaries:  [Monero Binaries](https://getmonero.org/downloads/)

- Step 1 : Download the [official binaries](https://getmonero.org/downloads/) or compile the last source available on [github](https://github.com/monero-project/bitmonero)

- Step 2 : Extract the files with the archive manager (same as winzip on Windows). Note the path where the files are (bitmonerod and simplewallet).

- Step 3 (only needed once): Open a terminal (ctrl+alt+t) and install the required dependencies by typing : "sudo apt-get install libboost-all-dev libssl-dev libevent-dev libdb++-dev"

- Step 4 (optional) : download the [blockchain](https://getmonero.org/downloads/) and save it in "/home/yourUserName/.bitmonero/"

- Step 5 : Open a terminal and load the path where your binaries are extracted (cf. step 2) by typing : "cd yourPathFromStep2"

- Step 6 : Load bitmonerod by typing in your terminal : "./bitmonerod". Wait for the synchronisation with the network (bitmonerod is updating the blockchain you have downloaded in step 4 or is downloading it from scratch). This can take a lot of time the first time, so be patient.

- Step 7 : Once bitmonerod is synchronised with the network, open a new terminal, change the directory (cf. step 5), and launch simplewallet by typing : "./simplewallet"

- Step 8 : Enter the name you want for your portfolio and follow the instructions from the terminal.

- Step 9 : to exit bitmonerod or simplewallet just type "exit" in the associated terminal.

Now to access the portfolio you have just created you will have to launch bitmonerod, wait for it to be synchronised with the network, launch simplewallet, and type the name of your portfolio and your password.

