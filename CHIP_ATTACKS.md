# TEE Chip Attacks: What does it take?

**tl;dr**: Chip attacks cannot be prevented, but only made expansive to carry on, which is very relative, depending on the application in which the chip is used. Furthermore, as far as I know, there's no known chip attack that has been reported along with its required cost. Hence, currently we can only speculate that an attack may be in the range of a 1 milltion dollars, judging from the cost of focused ion beam (FIB) microscopes and guessing how much money a team of experts would cost. In the context of crypto/web3, protocol designers should probably be extremely careful, given that many protocols move massive amounts of money; in the hundreds of millions, and more.

It would be extremely useful to see actual chip attacks being reported by research groups, as it would help to set a price on such attacks, and the price of the attack could be used by protocol designers.

---

By chip attacks here, we mean those described in [Intel SGX Explained], _section 3.4.3_. The paper is from 2016, and at the time of writing the authors wrote that the Intel's CPU had a [feature size](https://en.wikipedia.org/wiki/Semiconductor_device_fabrication#Feature_size) of 14nm. In the interest of being pro-active to understand current or future chips, we could assume [3nm](https://en.wikipedia.org/wiki/3_nm_process) feature size perhaps. But it's not clear what this exactly means, because apparently these numbers are more of a marketing act, as per https://en.wikipedia.org/wiki/3_nm_process:

> The term "3 nanometer" has no direct relation to any actual physical feature (such as gate length, metal pitch or gate pitch) of the transistors. According to the projections contained in the 2021 update of the [International Roadmap for Devices and Systems](https://en.wikipedia.org/wiki/International_Roadmap_for_Devices_and_Systems) published by IEEE Standards Association Industry Connection, a "3 nm" node is expected to have a contacted gate pitch of 48 nanometers, and a tightest metal pitch of 24 nanometers.[[12]](https://en.wikipedia.org/wiki/3_nm_process#cite_note-IRDS-12)
>
> However, in real world commercial practice, "3 nm" is used primarily as a marketing term by individual microchip manufacturers (foundries) to refer to a new, improved generation of silicon semiconductor chips in terms of increased transistor density (i.e. a higher degree of miniaturization), increased speed and reduced power consumption.[[13]](https://en.wikipedia.org/wiki/3_nm_process#cite_note-13)[[14]](https://en.wikipedia.org/wiki/3_nm_process#cite_note-14) There is no industry-wide agreement among different manufacturers about what numbers would define a "3 nm" node.[[15]](https://en.wikipedia.org/wiki/3_nm_process#cite_note-IRDS2-15)

In any case, it's quite clear that instrumentation to work at a smaller scale is needed.

Back to [Intel SGX Explained](https://eprint.iacr.org/2016/086), _section 3.4.3_, some key excerpts:

> The most equipment-intensive physical attacks involve removing a chip’s packaging and directly interacting with its electrical circuits. These attacks generally take advantage of equipment and techniques that were originally developed to diagnose design and manufacturing defects in chips. [[22]] covers these techniques in depth.
>
>The cost of chip attacks is dominated by the required equipment, although the reverse-engineering involved is also non-trivial. This cost grows very rapidly as the circuit components shrink. At the time of this writing, the latest Intel CPUs have a 14nm feature size, which requires ion beam microscopy.
>
> The least expensive classes of chip attacks are destructive, and only require imaging the chip’s circuitry. These attacks rely on a microscope capable of capturing the necessary details in each layer, and equipment for mechanically removing each layer and exposing the layer below it to the microscope.
>
>  E-fuses and polyfuses are particularly vulnerable to imaging attacks, because of their relatively large sizes.
>
> [...], once an attacker develops a process for accessing a module without destroying the chip's circuitry, the attacker can use the same process for both passive and active attacks.
>
> **At the architectural level, we cannot address physical attacks against the CPU’s chip package.** [...]
>
> Thankfully, **physical attacks can be deterred by reducing the value that an attacker obtains by compromising an individual chip. As long as this value is below the cost of carrying out the physical attack, a system's designer can hope that the processor's chip package will not be targeted by the physical attacks.**
>
> Architects can reduce the value of compromising an individual system by avoiding shared secrets, such as global encryption keys. Chip designers can increase the cost of a physical attack by not storing a platform's secrets in hardware that is vulnerable to destructive attacks, such as e-fuses.

> [[22]]: Friedrich Beck. _Integrated Circuit Failure Analysis: a Guide to Preparation Techniques._ John Wiley & Sons, 1998.

There's also a brief discussion of PUFs in a security analysis section of [Intel SGX Explained], section _6.6.2 Physical Attacks_:

> The threat model stated by the SGX design excludes physical attacks targeting the CPU chip (§ 3.4.3).  Fortunately, Intel’s patents disclose an array of countermeasures aimed at increasing the cost of chip attacks.
>
> For example, the original SGX patents [110, 138] disclose that the Fused Seal Key and the Provisioning Key, which are stored in e-fuses (§ 5.8.2), are encrypted with a global wrapping logic key (GWK). The GWK is a 128-bit AES key that is hard-coded in the processor’s circuitry, and serves to increase the cost of extracting the keys from an SGX-enabled processor.
>
> As explained in § 3.4.3, e-fuses have a large feature size, which makes them relatively easy to “read” using a high-resolution microscope. In comparison, the circuitry on the latest Intel processors has a significantly smaller feature size, and is more difficult to reverse engineer. **Unfortunately, the GWK is shared among all the chip dies created from the same mask, so it has all the drawbacks of global secrets explained in § 3.4.3.**
>
> Newer Intel patents [67, 68] describe SGX-enabled processors that employ a Physical Unclonable Function (PUF), e.g., [175], [133], which generates a symmetric key that is used during the provisioning process.
>
> Specifically, at an early provisioning stage, the PUF key is encrypted with the GWK and transmitted to the key generation server. At a later stage, the key generation server encrypts the key material that will be burned into the processor chip’s e-fuses with the PUF key, and transmits the encrypted material to the chip. The PUF key increases the cost of obtaining a chip’s fuse key material, as an attacker must compromise both provisioning stages in order to be able to decrypt the fuse key material.
>
> As mentioned in previous sections, patents reveal design possibilities considered by the SGX engineers. However, due to the length of timelines involved in patent applications, patents necessarily describe earlier versions of the SGX implementation plans, which might not match the shipping implementation. We expect this might be the case with the PUF provisioning patents, as it makes little sense to include a PUF in a chip die and rely on e-fuses and a GWK to store SGX’s root keys. Deriving the root keys from the PUF would be more resilient to chip imaging attacks.

I don't know whether the latest Intel SGX chips make use of PUFs, and how accurate the above still is for the latest chips.

In any case, it's quite clear that from the authors of [Intel SGX Explained], physical attacks cannot be "physically" prevented but can only be "economically" prevented. **Hence, chips are secure through economic incentives, not through physics.** If that is correct, using TEEs in a protocol calls for a very careful mechanism design where protocol designers take into account the cost of physically attacking the chip. For example, if we put a price tag of 1 million dollar in performing a chip attack, then a protocol using TEEs should make sure that less than 1 million dollars can be gained by performing a chip attack. Moreover, it is very important to take into account that this way of thinking does not consider attackers who wish to attack a protocol for non-economical reasons, such as breaking the privacy and/or anonymity of participants in the targeted protocol. In the case of such protocols, then it seems that current TEEs are simply not a reliable technology, as any attackers with sufficient funds and motivated to break the privacy and/or anonymity of a protocol, would be able to carry on the attack.

Now, with this background in mind, it seems that it would be extremely useful to see actual chip attacks being reported by research groups, as it would help to set a price on such attacks, and the price of the attack could be use by protocol designers.

[22]: https://www.wiley.com/en-ae/Integrated+Circuit+Failure+Analysis:+A+Guide+to+Preparation+Techniques-p-9780471974017
[Intel SGX Explained]: https://eprint.iacr.org/2016/086