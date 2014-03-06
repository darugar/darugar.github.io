---
layout: parand
title:  "Setting up pageant for password-less login"
date:   2006-11-13 10:00:00
categories: stddev
---
This is a recipe for setting up pageant.exe on windows to allow ssh login without having to type in the password every time. Mainly for my own notes.

From [putty](/web/20101222035752/http://www.chiark.greenend.org.uk/~sgtatham/putty/) [download](/web/20101222035752/http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html): putty.exe , puttygen.exe, pageant.exe .

Run pageant. Take the default options and move your mouse around till your key is generated.

Put in a passphrase and save the private key somewhere private. Save the public key.

Login to the remote host using putty.

vi ~/.ssh/authorized\_keys

Paste in the stuff from puttygen, the part that says "Public key for pasting into…"

Close puttygen. Run pageant.exe. A little terminal with a hat icon appears in your windows task bar area. Right click it. Select add key and add in your private key that you had saved earlier. It'll ask for a password, type it in.

That's it, you're done. Now you can putty to your remote host and it won't ask you for a password. Particularly useful for things like winscp, svn+ssh, etc.
