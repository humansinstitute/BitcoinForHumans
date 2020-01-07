# Host a Free BTC Pay Server

This could be done for development needs or as a routing or shop front end that you'd prefer to up and running 24x7.

We're going to take advantage of the Oracle Cloud Free Tier - which provides two free linux VMs (free forever is the )

Open a screen incase you get disconnected which will make it easier to retutrn to your session `screen -S btcpay`. (I had this first time trying to install... bit annoying.)

If you need to leave this session you can detach with `Ctrl+a` and if you get kicked out of the ssh session you can reattch with `screen -r btcpay`, [more details here](https://linuxize.com/post/how-to-use-linux-screen/).

Once you're in switch to root  `sudo SU`.

Then copy and paste in the following block (assuming you want mainnet BTC, plus LND).

```bash
export BTCPAY_HOST="btcpay.winn.cloud"
export NBITCOIN_NETWORK="mainnet"
export BTCPAYGEN_CRYPTO1="btc"
export BTCPAYGEN_REVERSEPROXY="nginx"
export BTCPAYGEN_LIGHTNING="lnd"
export BTCPAY_ENABLE_SSH=true
. ./btcpay-setup.sh -i
```

![](/Users/pwinn/code/humansinstitute/BitcoinForHumans/assets/2020-01-07-10-08-01-image.png)


