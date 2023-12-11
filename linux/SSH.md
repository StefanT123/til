# SSH

#### Flags
- `-N`: this lets SSH know that we’re not going to be sending any commands after the server
- `-f`: this sends SSH to the background. If we didn’t do this, our terminal would hang and we wouldn’t be able to use it
- `-L`: tells SSH to forward a local port
- `-R`: tells SSH to forward a remote port
- `-D {port}`: tells SSH to create a dynamic local port to send our traffic through.
- `-J`: jump through hosts
- `-A`: allows you to forward your key agent to the machine you're connecting to, allowing you to use your private keys from the machine you're connected to
- `-t`: quickly run commands on a remote server that require some sort of interaction such as `Vim` or `top`
- `-g`: this tells SSH to allow remote hosts to connect to locally forwarded ports
- `~?`: help menu

### Local Port Forwarding (-L)

Like the name implies, local port forwarding allows you to create a local port that is forwarded to a remote port. Let’s assume that the server `internal-web.int` is hosting a webpage that is only accessible on the loopback interface. This means that in order for us to access that webpage, we must be on `internal-web.int`. One way that we can get around this is by using an SSH local port forward. Assuming we SSH access to `internal-web.int`, on the host machine `campfire.int`, we can create a local forward that will allow us to access the remote webserver via a local port.

The command to do this is: `ssh -N -f -L 1337:127.0.0.1:80 root@internal-web.int`. This command is ran on `campfire.int`. Now that we have established the local port forward, we can interact with port 80 on `internal-web.int` by sending requests to port `1337` on our local machine `(campfire.int)`.

### Remote Port Forwarding (-R)

Remote port forwarding is the opposite of local port forwarding. Lets assume that we have access to `internal-web.int` and it is hosting a webpage that is only accessible on the loopback interface. Lets also assume that `campfire.int` cannot directly access `internal-web.int`. In this scenario we’d like to access `internal-web.int` from `campfire.int`. The problem is that we cannot directly communicate between `campfire.int` and `internal-web.int` due to a firewall. To get around this, we identify that `vuln-server.int` is reachable by both `campfire.int` and `internal-web.int`. The solution in this case is to use remote port forwarding SSH option to forward the port `80` from `internal-web.int` to an arbitrary port on `vuln-server.int`. Once we complete the remote port forward, we should be able to access the `internal-web.int`’s internal web page running on port `80` by issuing a curl command to `vuln-server.int`.

The command to do this is: `ssh -N -f -R 3000:127.0.0.1:80 root@vuln-server.int`. Now that we have established the remote port forward, we can access port `80` on `internal-web.int` by sending a curl request to `vuln-server.int:3000`.

### Dynamic Port Forwarding (-D)

Dynamic port forwarding with the -D option is an interesting option for proxying traffic over a SOCKS proxy. Lets assume that `internal-web.int` is hosting a web application that is only accessible on the internal network. We will assume that we have SSH access to `vuln-server.int` and it is on the same internal network and able to reach `internal-web.int`. What we would like to accomplish is accessing the webserver running on `internal-web.int` by proxying all of our traffic from `campfire.int` through `vuln-server.int` using both `proxychains` and our local web browser. First, we must ensure the `/etc/proxychains.conf` configuration file is set correctly.

```bash
[ProxyList]
# add proxy here...
# meanwhile
# defaults set to "tor"
socks5 127.0.0.1 8080

# Socks5: Tells proxychains to use socks5 (instead of socks4)
# 127.0.0.1: Tells proxychains to use our localhost
# 8080: Is the port we will use for our dynamic forward. This must match the port you specify with -D in your SSH command.
```

The command to do this is `ssh -N -f -D 8080 root@vuln-server.int`. After creating the dynamic port forward over port `8080` and setting `socks5 127.0.0.1 8080` in `/etc/proxychains.conf`, we can now run `proxychains curl 192.168.1.185` and see our webpage hosted on `192.168.1.185`.


### Jumphosts (-J)

Compared to the previous commands, jumping through hosts with SSH is fairly straight forward. In this scenario we will proxy our traffic through two hosts to reach a destination host that is not reachable by our current host `campfire.int`. Our jump chain will look like this: `campfire.int` -> `vuln-server.int` -> `internal-web.int` -> `dns.int`.

The command to do this is `ssh -J root@vuln-server.int,root@internal-web.int root@dns.int`. Note that multiple jumps are separated by commas.


### Agent Forwarding (-A)

The SSH agent allows you to add private keys/identities to the agent running on your local machine using `ssh-add <private_key_file>`. These keys can then be listed with `ssh-add -l`. After adding a key to the `ssh-agent` utility, you can then SSH to a server using the key without having to re-enter the password. This is useful for both humans and service accounts. The -A option allows you to forward your key agent to the machine you're connecting to, allowing you to use your private keys from the machine you're connected to.


### TTY Command Allocation (-t)

This option is super simple but very helpful for quickly running commands on a remote server that require some sort of interaction such as `Vim` or `top`. My favorite use case for this is when I need to quickly edit a file on a remote server. All you need to do is run the command `ssh root@internal-web.int -t top` and you will be greeted with a TTY containing the top command.


### Global port (-g)

This one is a bit less common, but it allows us to define a locally forwarded port as a "global port" that will allow us to proxy and traffic coming in on a local port to a port on an external server. This is similar to the `-L`option mentioned previously, but it will allow us to access the "Local" ports from an external machine. In the scenario below we have shell access to `vuln-server.int` and we would like to proxy any connection hitting port `2222` to port `22` on `internal-web.int`.

The command to do this is: `ssh -N -f -g -L 2222:localhost:22 root@internal-web.int`. Even though our initial SSH command was to port 2222 on `vuln-server.int`, our shell tells us that we are actually on `internal-web.int` because of the `ssh -N -f -g -L 2222:localhost:22 root@internal-web.int`


### SSH Console (~?)

```
Supported escape sequences:
 ~.   - terminate connection (and any multiplexed sessions)
 ~B   - send a BREAK to the remote system
 ~C   - open a command line
 ~R   - request rekey
 ~V/v - decrease/increase verbosity (LogLevel)
 ~^Z  - suspend ssh
 ~#   - list forwarded connections
 ~&   - background ssh (when waiting for connections to terminate)
 ~?   - this message
 ~~   - send the escape character by typing it twice
(Note that escapes are only recognized immediately after newline.)
```

The SSH console is a "hidden" feature of SSH that allows you to exert some control over SSH without having to interact with the remote system. This is useful if you’re trying to control SSH itself but your shell is broken. To access the help menu for the console press `~?`. If you’re familiar with `vim`, this is similar to using the leader character. This will bring up the help console. There are two options that I find very useful. First is the `~.` option which will kill your session (very useful if you’ve broken something).

The second is the "Console" option which can be accessed with `~C`. This console has a few options for forwarding. If you find that you’ve SSH’d into a server and would like to begin using this session as a port forward session (such as a dynamic forward with the -D option mentioned previously), you can forward this session with the `-D 8080` option to create a forward-on-the-fly out of this session.


### SSH Config

The SSH config file is located at `~/.ssh/config` and can be utilized to save you time when making connections over SSH. The config file uses a very easy to follow syntax that allows you to save your SSH configuration instead of having to type out all the options you want in the command line each time. SSH will parse this file when making an SSH connection. If the server you’re connecting to has an configuration defined in `~/.ssh/config`, it will use that configuration. Note that command line parameters take precedence over the configuration file. This means that if your `~/.ssh/config` file says that the user for `internal-web.int` should be `root`, but you run the SSH command `ssh stefan@internal-web.int`, SSH will attempt to log you in as `stefan`, not `root.` Below is an example of a very basic `~/.ssh/config file`.

```bash
# You can put comments with a `#` at the beginning of the line only. 
host internal-web.int
    User root
    IdentityFile /home/ste46fan/ssh_agent/internal-web-no-pw
	Port 2222
```

### SSH Config Keywords

- `IdentityFile /path/to/private_key`: Allows you to specify the private key you wish to use for the host. Same as using -i
- `ForwardAgent`: This is the same as running ssh -A
- `ProxyJump root@internal-web.int`: Specify a server to proxy traffic through. Same as the `-J` option mentioned above.
- `Match`: This one is a bit more complex. The Match keyword allows you to define conditions in your SSH config. In the below example, SSH executes the command `export | grep PROXYME=TRUE`. If the program returns with a status code of 0 (in this case, meaning grep found a match), it will utilize the SSH keywords defined under the Match block (In this case, ProxyJump). Otherwise only the normal host `internal-web.int` block is used.


### ssh-copy-id

The `ssh-copy-id` utility is a small tool that allows us to quickly upload our public key to a server.

The command to do this is: `ssh-copy-id -i internal-web root@internal-web.int`