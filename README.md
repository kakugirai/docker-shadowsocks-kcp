#### Quick Start
To start shadowsocks, run `$ docker run -d -p8000:8000 -p8000:8000/udp -p9000:9000/udp kakugirai/sskcp`, this will start shadowsocs at `port:10800` with kcptun at `port:9000` in server mode. Use `--crypt none --mode fast --mtu 1400 --sndwnd 1024 --rcvwnd 1024 --parityshard 0 --nocomp` as the command line arguments of your kcptun client.

#### Enable `BBR congestion control algorithm`
For one use kernel version `>= 4.9`, should enable `TCP_CONG_BBR` in your host os in order to get a better network performance (especially in high packet-loss situation).

#### Usage
`$ docker run -it --rm luxrck/shadowsocks-kcp --help`

	shadowsocks-kcp uses server mode with kcptun enabled by default

	Options:
		-c|--client    start in client mode
		--no-kcp       disable kcptun

#### Environments
Change these environments list below to apply new settings.

##### privoxy
Set `PORT` to an non-zero value to enable privoxy http proxy (only avaliable in client mode).

Env.         | Val.
-------------|--------
PORT         | 0

##### shadowsocks-libev
Shadowsocks with `-u (udp relay)`, `--fast-open (tcp fast-open)` enabled.

Env.         | Val.
-------------|--------
SS_PORT      |10800
SS_LOCAL_PORT|1080
SS_PASSWORD  |123456
SS_METHOD    |chacha20
SS_TIMEOUT   |600
SS_SERVER    |0.0.0.0

##### kcptun
kcptun with `--crypt none`, `--nocomp` enabled.
Make sure to change client's command line arguments if you change these.

Env.           | Val.
---------------|--------
KCP_PORT       | 9000
KCP_MODE       | fast
KCP_MTU        | 1350
KCP_SNDWND     | 1024
KCP_RCVWND     | 1024
KCP_DATASHARD  | 10
KCP_PARITYSHARD| 0
