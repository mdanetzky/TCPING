# TCPING

Copy of [TCPING](https://elifulkerson.com/projects/tcping.php) by [Eli Fulkerson](https://elifulkerson.com/) version from December 30 2017.\
It was adopted to the 2019 version of Visual Studio Tools and enhanced by a new option --fail which allows it to run until the first failed socket read.\
This option is useful for running of legacy windows services in wine in Docker.

## Original description

```console
NAME
    tcping - simulate "ping" over tcp by establishing a connection to network hosts.
    Measures the time for your system to [SYN], receive the target's [SYN][ACK] and send [ACK].  Note that the travel time for
    the last ACK is not included - only the time it takes to be put on the wire a tthe sending end.

SYNOPSIS
    tcping [-tdsvf46] [-i interval] [-n times] [-w interval] [-b n] [-r times][-j depth] [--tee filename] [-f] destination [port]

DESCRIPTION
    tcping measures the time it takes to perform a TCP 3-way handshake (SYN, SYN/ACK, ACK) between itself and a remote host.
    The travel time of the outgoing final ACK is not included, only the (minimal) amount of time it has taken to drop it on
    the wire at the near end.  This allows the travel time of the (SYN, SYN/ACK) to approximate the travel time of the
    ICMP (request, response) equivalent.

OPTIONS
    -4      Prefer using IPv4

    -6      Prefer using IPv6

    -t      ping continuously until stopped via control-c

    -n count
            send _count_ pings and then stop.  Default 4.

    -i interval
            Wait _interval_ seconds between pings.  Default 1.  Decimals permitted.

    -w interval
            Wait _interval_ seconds for a response.  Default 2.  Decimals permitted.

    -d      include date and time on every output line

    -f      Force sending at least one byte in addition to making the connection.

    -g count
            Give up after _count_ failed pings.

    -b type
            Enable audible beeps.
            '-b 1' will beep "on down".  If a host was up, but now its not, beep.
            '-b 2' will beep "on up".  If a host was down, but now its up, beep.
            '-b 3' will beep "on change".  If a host was one way, but now its the other, beep.
            '-b 4' will beep "always".

    -c      only show output on a changed state

    -r count
            Every _count_ pings, we will perform a new DNS lookup for the host in case it changed.

    -s      Exit immediately upon a success.

    --fail  Exit immediately upon a failure.

    -v      Print version and exit.

    -j      Calculate jitter.  Jitter is defined as the difference between the last response time and the historical average.

    -js depth
            Calculate jitter, as with -j but with an optional _depth_ argument specified. If _depth_ is specified tcping will
            use the prior _depth_ values to calculate a rolling average.

    --tee _filename_
            Duplicate output to the _filename_ specified.  Windows can still not be depended upon to have a useful command line
            environment. Don't tease me, *nix guys.

    --file
            Treat the "destination" option as a filename.  That file becomes a source of destinations, looped through on a
            line by line basis.  Some options don't work in this mode and statistics will not be kept.


    destination
            A DNS name, an IP address, or (in "http" mode) a URL.
            Do not specify the protocol ("http://") in "http" mode.  Also do not specify server port via ":port" syntax.
            For instance:   "tcping http://www.elifulkerson.com:8080/index.html" would fail
            Use the style:  "tcping www.elifulkerson.com/index.html 8080" instead.

    port
            A numeric TCP port, 1-65535.  If not specified, defaults to 80.

    --header
            include a header with the command line arguments and timestamp.  Header is implied if using --tee.

HTTP MODE OPTIONS
    -h      Use "http" mode.  In http mode we will attempt to GET the specified document and return additional values including
            the document's size, http response code, kbit/s.
    -u      In "http" mode, include the target URL on each output line.

    --post  Use POST instead of GET in http mode.
    --head  Use HEAD instead of GET in http mode.
    --get   Shorthand to invoke "http" mode for consistency's sake.

    --proxy-server _proxyserver_
            Connect to _proxyserver_ to request the url rather than the server indicated in the url itself.
    --proxy-port _port_
            Specify the numeric TCP port of the proxy server.  Defaults to 3128.
    --proxy-credentials username:password
            Specify a username:password pair which is sent as a 'Proxy-Authorization: Basic' header.


RETURN VALUE
    tcping returns 0 if all pings are successful, 1 if zero pings are successful and 2 for mixed outcome.

BUGS/REQUESTS
    Please report bugs and feature requests to the author via contact information on http://www.elifulkerson.com

AVAILABILITY
    tcping is available at http://www.elifulkerson.com/projects/tcping.php
```
