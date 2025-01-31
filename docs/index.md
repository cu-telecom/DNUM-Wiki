<div style="text-align: left;">
  <img src="assets/full-logo-dark.svg" alt="My SVG Logo" width="400">
</div>

The **D**ns **NU**mber **M**apping (DNUM) project was born from a vague aspiration to create a publicly available [ENUM](https://datatracker.ietf.org/doc/html/rfc6116) platform to allow hobbyist telephony platforms to reach other directly over the public internet.

Several other popular hobbyist networks exist, but have quirks or use their own special sauce to function. The goal for DNUM is to use existing standards to provide simple, efficient and secure call routing - Namely SIP, ENUM, STIR/SHAKEN and DNSSEC.

Unfortunatly despite giving it some thought, a fully decentralised approach appears to be difficult to achive with the current vision of using certificates to secure and verify the various components. However, the ENUM specification supports delegation, which should allow for regional groups to operate semi-autonomously or independently.

For more information on the proposal, see the [Technical](./technical/index.md) section.

## Disclaimer

* This Wiki has been chucked together to gauge interest and start conversations. It's far from complete.
* At present this is just an experiment. It may never come to fruition, or die off like many other projects before it.
* Whilst the project is currently hosted on the [cutel.net](https://cutel.net) domain whilst we come up with a better name, DNUM isn't a CuTEL specific project.

## FAQ

* Why DNUM? - The name is a work in progress. If you've got a better one let us know.
* Why DNUM and not ENUM? - The RFC6116 explicitly states you can't use the term "ENUM" to describe a DDDS service for private numbering plans. Lame.
* But I'm happy using my existing network? - It's hoped we can offer a method of peering into existing networks, but it should also be possible to configure your system to interconnect with multiple networks. 
* Can I claim the same number I use on the PSTN? - On initial thought this should probably be avoided. If its available, you could claim the number, but we probably won't be reserving numbers, verifying ownership of the PSTN number, or encouraging the use of using DNUM to lookup PSTN numbers in the hope of reaching the right person.

## Contact Us

We're currently coordinating on the [CuTEL Discord Server](https://t.co/AixzjCUT9t)