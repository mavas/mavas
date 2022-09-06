# Docker compose Tor and I2P services

This `docker-compose.yml` file makes it easy to see how my production setups are built and deployed under the Tor and I2P networks, as services.

The `eotk` project is officially recommended and listed directly under the https://torproject.org URL prefix, and is used by at least a few news organizations, **so you know it's good quality to know this package**.  An alternative is using a Docker ubuntu image and the standar `tor` package, along with `superisord`.  There was a nifty github repo that had a nice and naive setup for a Tor Onion Service, and was perfect to fork and offers a new perspective on the Tor deployment that's different from `eotk`'s.  Both I think are sufficient though, and no other third option will be investigated.

I2P is impressive and was easy to get up and running, much more so than the 2 Tor examples above.
