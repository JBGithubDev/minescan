# FORK INFO

This is a fork of mat-1's fork of adrian154's fork of Robert David Graham's [MASSCAN](https://github.com/robertdavidgraham/masscan), with added support for pinging Minecraft servers and saving the response as a banner.

This fork *only* performs banner checking on Minecraft servers, works on any port, and contains an extended and updated exclude list.

# Building

On Debian/Ubuntu, it goes something like the following. It doesn't really have any dependencies other than a C compiler (such as gcc or clang).
```bash
sudo apt-get --assume-yes install git make gcc
git clone https://github.com/JBGithubDev/minescan
cd minescan
make
```

This puts the program in the masscan/bin subdirectory. To install it (on Linux) run:

```bash
make install
```

The source consists of a lot of small files, so building goes a lot faster by using the multi-threaded build. This requires more than 2gigs on a Raspberry Pi (and breaks), so you might use a smaller number, like -j4 rather than all possible threads.

```bash
make -j
```

# Usage

This is what the intended usage for this program looks like:
```bash
iptables -A INPUT -p tcp --dport 61000 -j DROP
masscan/bin/masscan -p25565 -oB mc-servers 0.0.0.0/0 --exclude-file masscan/data/exclude.conf --wait 10 --banners --rate 10000000 --source-port 61000
```
This will take about 12 hours on an 100 MB/s connection and will be about 700 MB in size.
