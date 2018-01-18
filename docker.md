# Docker notes

I put all of my files in ~/tmp, because one of the daemons is producing a bunch of data. I think it's btcd.

Also, the default cert btcd generates doesn't cover using "btcd" as the hostname. You'll need to generate that yourself.

Run `gen_btcd_cert.go` and it'll put rpc.cert and rpc.key in /tmp. Move those to ~/tmp/btcd_data/btcd and replace the cert/key files there.

Also follow the info in README.me (or the docs or whichever) for setting up btcd normally. The config file is in ~/tmp/btcd_data/btcd/.

btcd needs to be started before teller because it needs time to bind the rpc address.

Once you've got the certs and got btcd configured, you can start btcd first like:

$ docker-compose up -d btcd

(wait a bit, check btcd's logs to see some mention of port 8334)

Then configure teller. My config is my_config.toml. Also generate the btcd wallet as the README.md says.

Then:

$ docker-compose up -d

And then you should have access to teller's web interface on :7071 (and when we get the admin panel working, it'll be on :7711) and the rpc interface on :4121.

This setup isn't really feasible because btcd will ultimately need like 126gb of  space. So forget that.
