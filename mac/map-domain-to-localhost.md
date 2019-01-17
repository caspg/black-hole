## Mapping domain to localhost with ports

Run in the command line:

```bash
sudo ifconfig lo0 10.0.0.1 alias
echo "rdr pass on lo0 inet proto tcp from any to 10.0.0.1 port 80 -> 127.0.0.1 port 3000" | sudo pfctl -ef -

sudo ifconfig lo0 10.0.0.2 alias
echo "rdr pass on lo0 inet proto tcp from any to 10.0.0.2 port 80 -> 127.0.0.1 port 4000" | sudo pfctl -ef -
```

then edit `/etc/hosts`:

```
10.0.0.1 example.com
10.0.0.2 elixir.example.com
```

after saving `/etc/hosts` flush local dns cache:

```bash
dscacheutil -flushcache
```
