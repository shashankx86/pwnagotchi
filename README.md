# Pwnagotchi

<p align="center">
    <a href="https://github.com/aluminum-ice/pwnagotchi/releases/latest"><img alt="Release" src="https://img.shields.io/github/release/aluminum-ice/pwnagotchi.svg?style=flat-square"></a>
    <a href="https://github.com/evilsocket/pwnagotchi/blob/master/LICENSE.md"><img alt="Software License" src="https://img.shields.io/badge/license-GPL3-brightgreen.svg?style=flat-square"></a>
    <a href="https://github.com/evilsocket/aluminum-ice/graphs/contributors"><img alt="Contributors" src="https://img.shields.io/github/contributors/aluminum-ice/pwnagotchi"/></a>
    <a href="https://twitter.com/intent/follow?screen_name=pwnagotchi"><img src="https://img.shields.io/twitter/follow/pwnagotchi?style=social&logo=twitter" alt="follow on Twitter"></a>
</p>

This is a fork of the [original pwnagotchi project](https://github.com/evilsocket/pwnagotchi). I have heavily updated my fork to enable pwnagotchi to run well on a Raspberry Pi Zero 2 W. **I will not support the original RPiZW. The board is obsolete and unpowered. Spend $15 and get an RPiZ2W. Issues about the original RPiZW will be immediately closed.** Major changes include:

1. **Remove all dependency on Kali-Pi** (causes more problems than it fixes) :boom: :boom:
2. Update to [Old Stable Buster Lite 2023-05-03](https://downloads.raspberrypi.org/raspios_oldstable_lite_armhf/images/raspios_oldstable_lite_armhf-2023-05-03/)
3. Compile [nexmon from source](https://github.com/seemoo-lab/nexmon)
    * Raspberry Pi Zero 2W (RPiZ2W) supported via firmware patch bcm43436b0/9_88_4_65 (43430/2) and bcm43430a1/7_45_41_46 (43430/1)
    * Raspberry Pi 3B+ (RPi3B+) and Pi 4 (RPi4) supported via firmware patch bcm43455c0/7_45_206/
4. Update to [Go v1.21.5](https://go.dev/dl/)
5. Compile [BetterCap from source](https://github.com/bettercap/bettercap)
6. Install screenrc and [my preferred configuration for it](https://github.com/aluminum-ice/screenrc)
7. Install aircrack-ng
8. Install pwnagotchi plugin for the Waveshare UPS hat, Mastodon, and aircrack (to delete empty pcap files); need to manually add configuration to config.toml
9. Turn off power saving mode for the wifi chip to prevent BRCM firmware crashes during packet injection (e.g., deauth attack)

---

[Pwnagotchi](https://pwnagotchi.ai/) is an [A2C](https://hackernoon.com/intuitive-rl-intro-to-advantage-actor-critic-a2c-4ff545978752)-based "AI" leveraging [bettercap](https://www.bettercap.org/) that learns from its surrounding WiFi environment to maximize the crackable WPA key material it captures (either passively, or by performing authentication and association attacks). This material is collected as PCAP files containing any form of handshake supported by [hashcat](https://hashcat.net/hashcat/), including [PMKIDs](https://www.evilsocket.net/2019/02/13/Pwning-WiFi-networks-with-bettercap-and-the-PMKID-client-less-attack/), 
full and half WPA handshakes.

![ui](https://i.imgur.com/X68GXrn.png)

Instead of merely playing [Super Mario or Atari games](https://becominghuman.ai/getting-mario-back-into-the-gym-setting-up-super-mario-bros-in-openais-gym-8e39a96c1e41?gi=c4b66c3d5ced) like most reinforcement learning-based "AI" *(yawn)*, Pwnagotchi tunes [its parameters](https://github.com/evilsocket/pwnagotchi/blob/master/pwnagotchi/defaults.toml) over time to **get better at pwning WiFi things to** in the environments you expose it to. 

More specifically, Pwnagotchi is using an [LSTM with MLP feature extractor](https://stable-baselines.readthedocs.io/en/master/modules/policies.html#stable_baselines.common.policies.MlpLstmPolicy) as its policy network for the [A2C agent](https://stable-baselines.readthedocs.io/en/master/modules/a2c.html). If you're unfamiliar with A2C, here is [a very good introductory explanation](https://hackernoon.com/intuitive-rl-intro-to-advantage-actor-critic-a2c-4ff545978752) (in comic form!) of the basic principles behind how Pwnagotchi learns. (You can read more about how Pwnagotchi learns in the [Usage](https://www.pwnagotchi.ai/usage/#training-the-ai) doc.)

**Keep in mind:** Unlike the usual RL simulations, Pwnagotchi learns over time. Time for a Pwnagotchi is measured in epochs; a single epoch can last from a few seconds to minutes, depending on how many access points and client stations are visible. Do not expect your Pwnagotchi to perform amazingly well at the very beginning, as it will be [exploring](https://hackernoon.com/intuitive-rl-intro-to-advantage-actor-critic-a2c-4ff545978752) several combinations of [key parameters](https://www.pwnagotchi.ai/usage/#training-the-ai) to determine ideal adjustments for pwning the particular environment you are exposing it to during its beginning epochs ... but ** listen to your Pwnagotchi when it tells you it's boring!** Bring it into novel WiFi environments with you and have it observe new networks and capture new handshakes—and you'll see. :)

Multiple units within close physical proximity can "talk" to each other, advertising their presence to each other by broadcasting custom information elements using a parasite protocol I've built on top of the existing dot11 standard. Over time, two or more units trained together will learn to cooperate upon detecting each other's presence by dividing the available channels among them for optimal pwnage.

## Documentation

https://www.pwnagotchi.ai

## Links

&nbsp; | Official Links
---------|-------
Website | [pwnagotchi.ai](https://pwnagotchi.ai/)
Forum | [community.pwnagotchi.ai](https://community.pwnagotchi.ai/)
Slack | [pwnagotchi.slack.com](https://invite.pwnagotchi.ai/)
Subreddit | [r/pwnagotchi](https://www.reddit.com/r/pwnagotchi/)
Twitter | [@pwnagotchi](https://twitter.com/pwnagotchi)

## License

`pwnagotchi` is made with ♥  by [@evilsocket](https://twitter.com/evilsocket) and the [amazing dev team](https://github.com/evilsocket/pwnagotchi/graphs/contributors). It is released under the GPL3 license.
