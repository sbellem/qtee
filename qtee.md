# qTEE: Moving Towards Open Source and Verifiable Secure-through-Physics TEE Chips
This is an initiative to spark research to explore how we could develop a secure chip for TEEs (Trusted Execution Environments) that would ultimately be secure because of physics rather than economics[^1]. The chip design should be open source, and its physical implementation should be verifiable, meaning that it should match the open source design. Moreover, the root of trust (embedded secret key) should be proven to have not leaked during generation or manufacturing. Thus, the hope and vision is to develop a TEE chip that does not need to be trusted because it can be verified by physics and mathematics.

To put this vision into context, current TEEs such as Intel SGX, face the following challenges:

1. **NO proof of manufacturing** according to a known open source chip design specification
2. **NO proof of non-leakage of secret bits** -- how can we know that the secret bits (root of trust) encoded into the chip were not leaked at any point in time during manufacturing 
3. **NO proof of hidden-forever secret bits** -- above and beyond trusting or not trusting the chip manufacturers, and the manufacturing processes, one problem remains: Can we truly hide secret bits of information (root of trust) into physical matter?

See https://github.com/sbellem/qtee/issues/2, for more details[^2].


## Overview
The key topics that this document wishes to explore are:

* Revisiting the Problem which TEEs aim to solve
* Motivations for better TEEs
* Mobilization: How do we start?
    * Verifiable Chip based on an Open Source Hardware Design
    * Marching Towards DAMOs (aka Zero Trust Manufacturing)
    * Root of Trust with PUFs
* Do we really need TEEs? Could we do it all with mathematics (FHE, ZKP, MPC, etc)? 
* Beyond PUFs: Cryptography and Physics United


## The Problem TEEs aim to solve
TEEs are an attempt to solve the _secure remote computation_ problem. Quoting [Intel SGX Explained] by Victor Costan and Srinivas Devadas:

> Secure remote computation is the problem of executing software on a remote computer owned and maintained by an untrusted party, with some integrity and confidentiality guarantees.

Note that the remote computer is said to be owned and maintained by an _untrusted_ party. Yet, current TEEs, cannot handle physical attacks such as chip attacks (see [TEE Chip Attacks: What does it take?](https://hackmd.io/G7hetzQ7THGALpvx378VsQ)), which would allow an attacker to retrieve the root of trust (secret keys encoded in the hardware). Once an attacker knows the secret keys, it can emulate a TEE, and go through the attestation process unnoticed (e.g. see Appendix A. Emulated Guard eXtensions in https://sgx.fail/ paper).

Is it even possible to build a chip that can handle physical attacks, such as those making use of Focus Ion Beam microscopes as mentioned in [Intel SGX Explained] (section 3.4.3)? One could argue that it's not possible in the classical setting, but may be possible in the quantum setting. Some argue that PUFs (Physical Unclonable Functions) cannot be broken and would therefore be a solution. However, there's plenty of research that focuses of breaking PUFs, and there's also active research in developping more secure PUFs. Hence, it seems reasonable to assume that PUFs are not an ultimate solution to chip attacks, although they do seem to be a major improvement. (See [PUFs].)



## Motivation
According to [SoK: Hardware-supported TEEs] and [Intel SGX Explained], current chips that implement TEEs cannot protect against physical attacks such as chip delayering, which would allow an attacker to extract the so-called root of trust, meaning hardware embedded secret keys upon which the entire security of the TEE depends. The only current known defense against chip attacks is trying to make the cost of a chip attack as high as possible. To make things worst, it's not even clear what the cost of a chip attack is; perhaps one million dollar (see [CHIP ATTACKS])? So, at the very least, one would hope we would know what the cost of a chip attack is, such that protocol designers could [design mechanisms][mechanism design] that would eliminate economic incentives to attack the chip, because the cost of the attack would not be worth what could be extracted out of the attack. It's very important to note here that a protocol relying on TEEs may also be targeted for attacks for reasons other than financial, and it's probably best to avoid using TEEs for such cases (e.g. privacy preserving application used by political dissidents).

Aside from being vulnerable to chip attacks the current popular TEEs, such as Intel SGX, are closed source, meaning that their hardware designs are not public, which in turn makes it very difficult to know whether a chip is implemented as claimed. Even with an open source hardware design we would need to figure out how to verify that the chip was implemented as per the open source design, and that secrets generated and embedded into the hardware at the time of manufacturing were not leaked. 


### Don't Trust, Verify ... Or use TEEs?
In the crypto world, the motto "Don't Trust, Verify" is frequently used to emphasize the verifiability feature of the various protocols, which allows any user to verify for themselves the validity of a transaction or claim. It may be said that the backbone of the reverred verifiability is cryptography and distributed systems, which involves trusting mathematics and trusting an honest majority, respectively. Consensus protocols, and many multi-party computation (MPC) protocols require to trust that the majority of the validators are honest. The majority may range from 51% to 75% depending on the protocol. So on one hand the world of crypto is secured through a combination of mathematics and trust in an "honest majority". So what about TEEs? Where do they fit in this picture?

The so-called web3 world (aka as crypto space) increasingly makes use of TEEs (mostly Intel SGX) in applications where substantial amounts of money may flow, and where TEEs help secure the confidentiality of its users. It's therefore important to properly understand what it means to trust TEEs. For a strange reason, it seems complicated to answer the question of "What does it means to trust TEEs?" If you ask different people, you may find a spectrum of different answers ranging from the likes of: "You have to trust the chip maker! But you already trust them anyways." to "Intel SGX is broken every month, I don't understand why people use them!" In general, it may be fair to say that trusting a TEE means the following:

1. Trust that the chip is designed as per the claims of the chip maker.
2. Trust that the chip is manufactured as per the claims of the chip maker.
3. Trust that the root of trust is not leaked during the manufacturing process.
4. Trust that the root of trust cannot be extracted out "cheaply" or "easily" by an attacker who has physical access to the chip.

Note that the above implicitly assumes that the design and implementation are secure, free of bugs. The reasoning is that design and implementation flaws can be fixed and can happen whether the design is open source or not, whether the supply chain is correct, etc.



## Cypherpunk-Friendly Chip
As mentioned in [The Problem TEEs aim to solve](#The-Problem-TEEs-aim-to-solve), if the problem we wish to tackle is that of secure remote computation, the threat model should include attackers with physical access to the chip, which means that the chip should be secure against physical attacks, which may not even be possible in the classical setting (i.e. without using quantum physics). That being said, it does not mean that we cannot improve the current TEEs. This section aims to explore what we could feasibly do today to have a chip that attempts to align itself with the motto of "Don't Trust, Verify", omnipresent in the web3 and cypherpunk cultures.


### Verifiable Chip based on an Open Source Hardware Design
Having an open source hardware design is perhaps the most reasonable place to start. Verifying that a physical chip does implement the intended open source hardware design is perhaps more difficult, and we can try to tackle this in a second step. Hence, we'll first start by exploring how we could have a TEE chip with an open source hardware design.

#### Open Source Hardware Design
This is not a new idea, and it may be useful to survey current and past efforts such as:

* [Chips Alliance]
* [Caliptra]
* [Google Titan]
* [LibreSilicon]
* [The Silicon Salon]
 

#### Verfiable Chip Implementation
This is also not a new problem. One approach is to use [Logic Encryption], which somehow locks the chip design to protect against a  malicious foundry. The company [HENSOLDT Cyber] has numerous research works on the topic, in addition to actually making chips, and hence, is probably worth studying. Their papers are listed at https://hensoldt-cyber.com/scientific-papers/, but let's list a few here:

* [Scaling Logic Locking Schemes to Multi-Module Hardware Designs](https://www.ice.rwth-aachen.de/publications/publication/sisejkovicARCS2020/)
* [Inter-Lock: Logic Encryption for Processor Cores Beyond Module Boundaries](https://www.ice.rwth-aachen.de/publications/publication/sisejkovicETS2019/)
* [A Critical Evaluation of the Paradigm Shift in the Design of Logic Encryption Algorithms](https://www.ice.rwth-aachen.de/publications/publication/sisejkovicVLSIDAT2019/)
* [A Unifying Logic Encryption Security Metric](https://www.ice.rwth-aachen.de/publications/publication/sisejkovicSAMOS2018/)


 
#### References
* https://github.com/sbellem/qtee/issues/1
* https://github.com/sbellem/qtee/issues/2#issuecomment-1648191994



### Marching Towards DAMOs
refs: https://github.com/sbellem/qtee/issues/7

### Root of Trust with PUFs 
refs: https://github.com/sbellem/qtee/blob/main/PUFs.md


## Do we really need TEEs?
**Why can't we do it all with FHE, ZKP, and MPC?**

Not sure. :smile: Besides the performance limitations FHE, ZKP and MPC, the problem of proof-of-deletion or certified deletion may be the most mentioned one. The intuition is simple: "How do you prove that you completely forgot what some secret data was?" You could show that your harddisk has been completely wiped out, but perhaps you copied it elsewhere. Hence, certified deletion appears to not be possible in the classical setting but it apparently is if one is willing to step one foot (or two), into the quantum setting (e.g.: [Quantum encryption with certified deletion] by _Broadbent & Islam_, [Quantum Proofs of Deletion for Learning with Errors] by _Poremba_). If we are confined to the classical setting though, then TEEs may be useful. If the program generating and/or handling secrets is executed in a TEE then the program can be written such that it will delete the secrets once it's done with the task. As an alternative to TEEs, there's the idea of traceable secret sharing as presented in [Traceable Secret Sharing: Strong Security and Efficient Constructions] by _Boneh et al_.


## Beyond PUFs: Cryptography and Physics United
https://github.com/sbellem/qtee

### Trusted Black Hole Execution Environments
[Black Hole Computers](https://www.scientificamerican.com/article/black-hole-computers-2007-04/)



## Appendix: Intel SGX
If we take Intel as an example, trusting the chip manufacturer means many things. Intel SGX's so-called root of trust rests on two secret keys (seal secret and provisionaing secret), and an attestation key, as shown in the figure below, from [Intel SGX Explained]. Note that this may have changed since the writing of the [Intel SGX Explained] paper, but at the time at least, the two secrets were said to be stored in e-fuses inside the processor's die. Moreover, the two secret keys, stored in e-fuses, were encrypted with a global wrapping logic key (GWK). The GWK is a 128-bit AES key that is hard-coded in the processor's circuitry, and serves to increase the cost of extracting the keys from an SGX-enabled processor. The Provisioning Secret was said to be generated at the key generation facility - burned into the processor's e-fuses and stored in Intel's Provisioning Service DB. The Seal Secret was said to be generated inside the processor chip, and claimed not to be known to Intel. Hence, trusting Intel meant to trust that they do not leak the attestation key, and the provisioning key as they have access to them. Trusting Intel also meant that the manufacturing process that generates and embeds the Seal Secret did not leak the secret key. Trusting Intel also meant that once a chip is made, they did not attempt to extract the Seal Key, which is the only key, out of three, which they did not know.


![image](https://hackmd.io/_uploads/rydXhPCTa.png)




[^1]: Chips attacks cannot be prevented as of today (see [CHIP ATTACKS]). Making the cost of a chip attack expensive is the only current known defense mechanism. Thus, TEEs are ultimately only secure through economics.
[^2]:  Also, of relevance: https://github.com/sbellem/qtee/issues/1, https://github.com/sbellem/qtee/issues/7, https://github.com/sbellem/qtee/issues/8, [CHIP ATTACKS], and [PUFs].




[Intel SGX Explained]: https://eprint.iacr.org/2016/086
[SoK: Hardware-supported TEEs]: https://arxiv.org/abs/2205.12742
[mechanism design]: https://en.wikipedia.org/wiki/Mechanism_design
[CHIP ATTACKS]: https://github.com/sbellem/qtee/blob/main/CHIP_ATTACKS.md
[PUFs]: https://github.com/sbellem/qtee/blob/main/PUFs.md
[Chips Alliance]: https://github.com/chipsalliance
[Caliptra]: https://github.com/chipsalliance/caliptra
[Google Titan]: https://opentitan.org/
[LibreSilicon]: https://libresilicon.com/
[The Silicon Salon]: https://www.siliconsalon.info/
[Logic Encryption]: https://link.springer.com/chapter/10.1007/978-3-319-49019-9_3
[HENSOLDT Cyber]: https://hensoldt-cyber.com/
[Quantum encryption with certified deletion]: https://arxiv.org/abs/1910.03551
[Quantum Proofs of Deletion for Learning with Errors]: https://arxiv.org/abs/2203.01610
[Traceable Secret Sharing: Strong Security and Efficient Constructions]: https://eprint.iacr.org/2024/405