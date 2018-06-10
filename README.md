Utilities for working with `x2x`:

 *  `udisp`

    Use the lock files in `/tmp/.X11-unix` to list all X11 DISPLAY variables for a given user. Useful over SSH when DISPLAY points to the X proxy server of the ssh daemon.

 *  `run_on_service`

    Dispatch a command when a matching zeroconf service is added. Use this to add resiliency to a network client with automatic and immediate restarts. The command is never terminated; the client is expected to exit gracefully after the matching zeroconf service is removed.

Example:

 *  Place `run_on_service` on the client.

 *  Place `udisp` on the server along with the following scriptlet, `x2x-ssh`:

        h="$(hostname)"
        x2x -to "$(udisp $(whoami))" "$@" -label "$h" -title "x2x to ${h}"

 *  Run the following command after login, replacing `<MYSERVERNAME>` and `<MYUSERNAME>`:

        run_on_service '_ssh._tcp.local.' '<MYSERVERNAME>._ssh._tcp.local.' ssh -p'${port}' -XYCn '<MYUSERNAME>@${server}' 'x2x-ssh -west -wait -struts -nosel'"


License: GPL-3.0-or-later
