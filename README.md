Utilities for working with `x2x`:

 *  `udisp`

    Use the lock files in `/tmp/.X11-unix` to list all X11 DISPLAY variables for a given user. Useful over SSH when DISPLAY points to the X proxy server of the ssh daemon.

 *  `run_on_service`

    Repeatedly dispatch a command contingent upon the availability of a matching zeroconf service. Use this to add resiliency to a network client with automatic and immediate restarts. The command is never terminated; the client is expected to exit gracefully after the matching zeroconf service is removed.

 *  `x2x_loop`

    A wrapper that automatically relaunches `x2x`, which must exist in the PATH environment variable. This script waits for a valid X11 socket before relaunching `x2x`, and exits if the failure rate exceeds half the maximum possible failure rate over a time window of at least 10 runs. The script also exits if the X11 socket directory (`/tmp/.X11-unix`) is removed or it is unable to launch `x2x`. Use this to automatically restart `x2x` upon logging back in. When logging out both the actual display and the ssh X proxy display are closed, which terminates `x2x`. When called over ssh this script expects SIGHUP on connecion termination. See code for more information.

Example:

 *  Place `run_on_service` on the client.

 *  Place `x2x_loop` on the server.

 *  Run the following command on the client after login, replacing `<MYSERVERNAME>` and `<MYUSERNAME>`:

        run_on_service '_ssh._tcp.local.' '<MYSERVERNAME>._ssh._tcp.local.' ssh -p'${port}' -XYCn '<MYUSERNAME>@${server}' 'x2x_loop -west -wait -struts -nosel'"

 *  Script `udisp` is not required.


License: GPL-3.0-or-later
