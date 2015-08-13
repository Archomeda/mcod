# Reverse Proxy for Minecraft Servers

*This fork is an altered version of [mcod by Benjojo](https://github.com/benjojo/mcod).*

Minecraft uses a lot of memory, even when no one is actually in-game. This means
that it basically wastes precious memory resources when idle. But hey, welcome
to the wonderful world of Java.

In order to solve that, mcod can be used as a reverse proxy. In the background,
mcod manages the Minecraft server. The server will only be started when someone
actually logs into the server. The server will be automatically shut down after
a brief period of time when there's no one in-game anymore. The MotD will be
updated every time someone refreshes the server list and the server is actually
online. If the server is not online (a.k.a. idle), mcod will respond with a
cached version.

This version has some changes compared to the original code:
- Improved packet handling.
- Shows server status in the MotD (e.g. idle, starting).
- Supports ping packets.
- Refuses player logins when the server is not ready yet, instead of timing out.
  It will show a message explaining why the connection has failed.
- Improved logging.
- It has no configurable cached banner or strict mode anymore. Instead, it will
  detect everything automatically. Note that this is only supported for
  Minecraft 1.7 or higher (tested on version 1.7.10). Earlier versions are
  **not** compatible with this fork.

## Compilation
The language used for this application, is [Go](https://golang.org/).
```bash
$ cd mcod
$ go build
```

## Usage
Place `mcod`, `StartServer` and `StopServer` in the Minecraft directory. Edit
`StartServer` and `StopServer` to support your Minecraft server. Run `mcod`.

Type `./mcod -h` to get more information about the supported command line
arguments:
```
$ ./mcod -h
Usage of ./mcod:
  -backend="localhost:25567": The IP address that the MC server listens on when it's online
  -listen=":25565": The port / IP combo you want to listen on
```
