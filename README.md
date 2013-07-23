ComputerCraft APIs
==================

This repository contains a list of smaller APIs for [ComputerCraft][] computers and turtles, which I feel don't deserve their own repository.

[Startup API](apis/startup)
=============

This API provides an easy way of handling multiple startup scripts. Startup scripts will be stored in a configurable folder (default: `autorun`). You can add (`startup.addFile`, `startup.addScript`) and remove (`startup.remove`), as well as enable (`startup.enable`) or disable (`startup.disable`) single startup scripts via this API. In general, you'll want to load this API in your actual startup script and then call `startup.run`. See the [example startup file](startup).

You can interact with this API from the shell by using the [startup-conf](programs/startup-conf) program.

[Daemon API](apis/daemon)
============

This API provides an easy way of handling [daemons][] (or services, if you prefer). Daemon scripts will be stored in a configurable folder (default: `daemons`). Similar to the startup API, daemons can be added and removed, as well as enabled and disabled via the API. You can also start (`daemon.start`) and stop (`daemon.stop`, `daemon.kill`) daemons via the API. Daemons will always run in the background, and will, in particular, not interfere with the terminal (unless explicitly using the `term` API).

You can interact with this API from the shell by using the [daemon-conf](programs/daemon-conf) program.

[Stacktrace](apis/stacktrace)
============

This API provides a single function, `stacktrace.tpcall`, which is functionally the same as `pcall`, except that it will provide a full stacktrace instead of just the exact error location. I find it useful to hook it in as a replacement for `pcall` in my startup script.

Example startup script
======================

This is an [example startup script](startup) (placed in the root folder, so this would be the "original" startup file) loading and initializing the APIs.

Installation
============

Sorry, but I'm too lazy to maintain pastebin versions of these. You'll have to manually download and install these scripts.


[computercraft]: http://www.computercraft.info/
[daemons]: http://en.wikipedia.org/wiki/Daemon_(computing)