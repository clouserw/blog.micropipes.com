Here are some step by step instructions for enabling encryption using 
[crypt.py](https://weechat.org/scripts/source/crypt.py.html/) in weechat.

First, ensure the crypt.py script is installed.  The easiest way is from within weechat itself:

    /script install crypt.py
    /script autoload crypt.py

You should see some simple messages saying crypt.py was installed and enabled for automatic loading.  

Next you need to generate an encryption key.  This just needs to be named with the channel you want to use the key with (I use #channel below).  For example:

    cd .weechat
    openssl genrsa -out cryptkey.#channel 4096

We might as well make sure only we can read it:

    chmod 600 cryptkey.#channel

At this point typing any text in #channel will automatically be encrypted (use a second client if you'd like to verify it).  For example, I typed:

    1811 clouserw │ testo

And the other clients in #channel see:

    1811 clouserw | +qRy3GsV2sPRlJSdP1IqqV|
  
The next step is to distribute the key to the other people who will need to decrypt the chat.  Take a minute to consider the best way to do this as the chat will only be as secure as this key.

Lastly, you can optionally add an indicator to the status bar by adding 'encrypted' to weechat.bar.status.items.  This command will tell you your current value:

    /set weechat.bar.status.items

Copy that value and add 'encrypted' where you'd like it to show up.  Mine is:

    /set weechat.bar.status.items "[time],[buffer_count],[buffer_plugin],buffer_number+:+buffer_name+{buffer_nicklist_count}+buffer_filter,encryption,[lag],[hotlist],completion,scroll"
    
which looks like this:

    [18:16] [32] [irc/freenode] 30:#channel{3}⚑ (encrypted)  [H: 3, 4, 5, 6]

That's all there is too it!
