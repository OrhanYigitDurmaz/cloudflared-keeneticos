Since keendns is ran on keenetic's own servers, i dont trust them.
Well, i dont trust anyone, its just that i dont trust keeneticos as much as cloudflare.
This is just me trynig to run cloudflared on top of opkg.

After searching github for efforts, everything i found was only compiled for mipsle (little endian.)

But i have a KN-3610, this is a big endian device!

So i cloned the repo, changed ARCH to mips, and crossed my fingers.

First build was unsuccessful, but that was just an environemtn variable.

After fixing that, ran it again aaaannnnddd...

It compiled.


Uploaded it to my router, tried to run the script aaaand. it failed.

After that i tried to run the cloudflared directly, and that gave me the error code i was looking for:

~ # /opt/usr/bin/cloudflared
unable to find config file
~ # /opt/usr/bin/cloudflared service install
mkdir /etc/cloudflared: read-only file system

And i tried to run it how loudflare inteneded it to be:

~ # /opt/usr/bin/cloudflared service install <your_token_here>
2025-03-27T20:00:26Z INF Using SysV
2025-03-27T20:00:26Z ERR error generating system template error="error creating /etc/init.d: mkdir /etc/init.d: read-only file system"
error creating /etc/init.d: mkdir /etc/init.d: read-only file system

Welp. I guess i have to make it somehow append every directory with /opt .
