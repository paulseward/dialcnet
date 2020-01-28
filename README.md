dialcnet
========

Asterisk Subroutine for passing calls to the CNet collectors network of asterisk servers.  For more details about CNet, see https://www.ckts.info/

This version is based on work by Chad Perkins, with some features taken from a version written by Tele706 (Brian)

It's been tidied up a bit by Paul Seward, and is a bit better about sanitizing input passed by the caller than previous versions.

This version lives at: https://github.com/paulseward/dialcnet

Installation
------------

- Copy dialcnet.conf to /etc/asterisk
- Add a fragment to /etc/asterisk/extensions.conf which "includes" the dialcnet code

```
#include "dialcnet.conf"
```

- Add a dialplan rule which passes calls to the subroutine if they look like they're headed for CNet

```
exten => _X.,1,noop(CNET-outgoing context from ${CALLERID(all)} to ${EXTEN})
exten => _X.,n,Set(CALLERID(all)="My Default Outgoing CallerID" <1234567890>);
exten => _X.,n,Gosub(dialcnet,start,1(${EXTEN}))
exten => _X.,n,Hangup()
```
