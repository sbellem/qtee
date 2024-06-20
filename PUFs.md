# Introduction to PUFs
[Physical Unclonable Functions](https://en.wikipedia.org/wiki/Physical_unclonable_function) are arguably the current best hope to protect against physical attacks aimed at extracting secret keys (root of trust). That being said, PUFs are an active area of research where new PUFs design are proposed and existing designs are broken. Hence, research is needed to better understand the limitations of PUFs in the context of TEEs.

The first PUFs was presented in the PhD thesis titled 
[Physical one-way functions](https://dspace.mit.edu/handle/1721.1/45499), by Ravikanth Srinivasa Pappu.


Not sure where it's best to start, but perhaps this article (if you have access):  
[Physical unclonable functions](https://www.nature.com/articles/s41928-020-0372-5) by [Yansong Gao](https://www.nature.com/articles/s41928-020-0372-5#auth-Yansong-Gao-Aff1-Aff2), [Said F. Al-Sarawi](https://www.nature.com/articles/s41928-020-0372-5#auth-Said_F_-Al_Sarawi-Aff3) & [Derek Abbott](https://www.nature.com/articles/s41928-020-0372-5#auth-Derek-Abbott-Aff4)

OR:

* [Physical Unclonable Functions for Device Authentication and Secret Key Generation](https://people.csail.mit.edu/devadas/pubs/puf-dac07.pdf)

  > Because the PUF circuit is rather simple, attackers can try to construct a precise timing model and learn the parameters from many input-output pairs [8]. To prevent these model-building attacks, the PUF circuit output can be obfuscated by XOR’ing multiple outputs or a PUF output can be used as one of the MUX control signals. **Note that the model building attack is irrelevant for the cryptographic key generation where the PUF output is never directly exposed.** [G. Edward Suh, Srinivas Devadas](https://people.csail.mit.edu/devadas/pubs/puf-dac07.pdf)

* [An Introduction to Physically Unclonable Functions](https://www.allaboutcircuits.com/technical-articles/an-introduction-to-physically-unclonable-functions/)

  > When manufactured, the PUF will be fed a series of different challenges and have its responses recorded. Through this exercise, the designers know each PUF's unique response to a given challenge and can use this information to prevent counterfeiting, create and store cryptographic keys, and many other security feats.
  
  TODO: figure out if the set of CRPs is not needed for signing keys. Also, out of curiosity could there be oblivious (or zk) CRPs, meaning that no one knows the challenge response pairs, but yet, they can be used.
  

# First well-known PUF: Physical One-Way Functions
https://www.science.org/doi/full/10.1126/science.1074376

Also at https://nbviewer.org/github/rpappu/pdf-publications/blob/master/Pappu-Science-2002.pdf


## Taxonomy of PUFs
Main reference: https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy

![image](https://hackmd.io/_uploads/r19_7exI0.png)


![image](https://hackmd.io/_uploads/HJdtVgxUA.png)


Images source: [A PUF taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy) by McGrath et al.

<table>
    <thead>
        <tr>
            <th>Concept</th>
            <th>Mechanism</th>
            <th>Parameter</th>
            <th>Implicity</th>
            <th>Evaluation</th>
            <th>Family</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <b><a href="https://ieeexplore.ieee.org/abstract/document/1346548">
                    Arbiter PUF
                </a></b>
            </td>
            <td rowspan=28>All-electronic</td>
            <td rowspan=2>Time</td>
            <td rowspan=16>Implicit</td>
            <td rowspan=16>Intrinsic</td>
            <td rowspan=3>Racetrack</td> 
        </tr>
        <tr>
            <td>ClockPUF</td>
        </tr>
        <tr>
            <td>
                <b>
                    <a href="https://dl.acm.org/doi/abs/10.1145/586110.586132">
                        Ring oscillator PUF
                    </a>
                </b>
            </td>
            <td rowspan=2>Frequency</td>
        </tr>
        <tr>
            <td>TERO PUF</td>
            <td rowspan=2>Transient/glitch</td>
        </tr>
        <tr>
            <td>GlitchPUF</td>
            <td rowspan=2>Voltage/current</td>
            </tr>
        <tr>
            <td>
                <b>
                    <a href="https://link.springer.com/chapter/10.1007/978-3-540-74735-2_5">
                        SRAM failure PUF
                    </a>
                </b>
            </td>
            <td rowspan=6>Volatile memory</td>
        </tr>
        <tr>
            <td>Bistable ring PUF</td>
            <td rowspan=5>Bistable state</td>
        </tr>
        <tr>
        	<td>DRAM PUF</td>
        </tr>
        <tr>
        	<td>MECCA PUF</td>
        </tr>
        <tr>
        	<td>Rowhammer PUF</td>
        </tr>
        <tr>
        	<td>SRAM PUF</td>
        </tr>
        <tr>
        	<td>CNN PUF</td>
        	<td rowspan=4>Voltage/current</td>
        	<td rowspan=14>Direct characterisation</td>
        </tr>
        <tr>
            <td>Power distro. PUF</td>
        </tr>
        <tr>
            <td>QUALPUF</td>
        </tr>
        <tr>
            <td>TV PUF</td>
        </tr>
        <tr>
            <td>VIA PUF</td>  
            <td rowspan=3>Binary connectivity</td>
        </tr>
        <tr>
            <td>NEMS PUF</td>
            <td rowspan=12>Explicit</td>
            <td rowspan=26>Extrinsic</td>
        </tr>
        <tr>
            <td>Self-assembly PUF</td>
        </tr>
        <tr>
            <td>CN PUF</td>
            <td rowspan=4>Voltage/current</td>
        </tr>
        <tr>
            <td>MEMS PUF</td>
        </tr>
        <tr>
            <td>Q EPUF</td>
        </tr>
        <tr>
            <td>SHIC PUF</td>
        </tr>    
        <tr>
            <td>BoardPUF</td> 
            <td rowspan=2>Capacitance</td>
        </tr>
            <tr>
      <td>Coating PUF</td>
    </tr>
    <tr>
      <td>Acoustical PUF</td>
      <td>Frequency</td>
    </tr>
    <tr>
      <td>Memristor PUF</td>
      <td rowspan=3>Bistable state</td>
      <td rowspan=3>Non-volatile memory</td>
    </tr>
    <tr>
      <td>PCKGEN</td>
    </tr>
    <tr>
      <td>STT-MRAM PUF</td>
    </tr>
    <tr>
      <td>CD PUF</td>
      <td rowspan=11>Hybrid (optical)</td>
      <td rowspan=9>Light intensity</td>
      <td rowspan=2>Implicit</td>
      <td rowspan=11>Optical</td>
    </tr>
    <tr>
      <td>Paper PUF</td>
    </tr>
    <tr>
      <td>Nanowire distro. PUF</td>
      <td rowspan=11>Explicit</td>
    </tr>
    <tr>
      <td>Optical fibre PUF</td>
    </tr>
    <tr>
      <td>Optical PUF</td>
    </tr>
    <tr>
      <td>Phosphor PUF</td>
    </tr>
    <tr>
      <td>Nanoparticle distro. PUF</td>
    </tr>
    <tr>
      <td>Monolayer depo. PUF</td>
    </tr>
    <tr>
      <td>Lanthanide lum. PUF</td>
    </tr>
    <tr>
      <td>Q OPUF</td>
      <td>Intensity and Frequency</td>
    </tr>
    <tr>
      <td>Liquid crystal PUF</td>
      <td>Frequency</td>
    </tr>
    <tr>
      <td>LC PUF</td>
      <td rowspan=2>Hybrid (RF)</td>
      <td rowspan=2>RF power absorption</td>
      <td rowspan=2>RF</td>
    </tr>
    <tr>
      <td>RF-DNA PUF</td>
    </tr>
    <tr>
      <td>Magnetic PUF</td>
      <td>Hybrid (magnetic)</td>
      <td>Mag. field</td>
      <td>intensity</td>
      <td>Implicit</td>
      <td>Magnetic</td>
    </tr>
    </tbody>
</table>

Table source: [A PUF taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy) by McGrath et al.

### Commercial PUFs

##### Commercial PUFS

<table>
    <thead>
        <tr>
            <th>Concept</th>
            <th>Mechanism</th>
            <th>Parameter</th>
            <th>Implicity</th>
            <th>Evaluation</th>
            <th>Family</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <b><a href="https://ieeexplore.ieee.org/abstract/document/1346548">
                    Arbiter PUF
                </a></b>
            </td>
            <td rowspan=7>All-electronic</td>
            <td rowspan=1>Time</td>
            <td rowspan=6>Implicit</td>
            <td rowspan=6>Intrinsic</td>
            <td rowspan=2>Racetrack</td> 
        </tr>
        <tr>
            <td>
                <b>
                    <a href="https://dl.acm.org/doi/abs/10.1145/586110.586132">
                        Ring oscillator PUF
                    </a>
                </b>
            </td>
            <td rowspan=1>Frequency</td>
        </tr>
        <tr>
            <td>
                <b>
                    <a href="https://link.springer.com/chapter/10.1007/978-3-540-74735-2_5">
                        SRAM PUF
                    </a>
                </b>
            </td>
            <td rowspan=1>Bistable state</td>
            <td rowspan=1>Volatile memory</td>
        </tr>
        <tr>
            <td>
                <b>
                    <a href="https://dl.acm.org/doi/abs/10.1145/1629911.1630089">
                    Power distro. PUF
                    </a>
                </b>
            </td>
        	<td rowspan=2>Voltage/current</td>
        	<td rowspan=4>Direct characterisation</td>
        </tr>
        <tr>
            <td>
                <b>
                    <a href="https://ieeexplore.ieee.org/abstract/document/839821">
                        TV PUF
                    </a>
                </b>
            </td>
        </tr>
        <tr>
            <td>VIA PUF</td>  
            <td rowspan=1>Binary connectivity</td>
        </tr>
        <tr>
            <td>Q EPUF</td>
            <td rowspan=1>Voltage/current</td>
            <td rowspan=2>Explicit</td>
            <td rowspan=2>Extrinsic</td>
        </tr>
    <tr>
        <td>Q OPUF</td>
        <td rowspan=1>Hybrid (optical)</td>
        <td>Intensity and Frequency</td>
        <td rowspan=1>Optical</td>
    </tr>
    </tbody>
</table>

Partial table source: [A PUF taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy) by McGrath et al.


## Remote Attestation
* [A lightweight remote attestation using PUFs and hash-based signatures for low-end IoT devices](https://www.sciencedirect.com/science/article/pii/S0167739X23002236)
* [SMART: Secure and Minimal Architecture for (Establishing a Dynamic) Root of Trust](https://ics.uci.edu/~gts/paps/smart.pdf)

## Malicious PUFs
* [Feasibility and Infeasibility of Secure Computation with Malicious PUFs](https://eprint.iacr.org/2015/405)
* [On the Security of PUF Protocols under Bad PUFs and PUFs-inside-PUFs Attacks](https://eprint.iacr.org/2016/322)
* [Everlasting UC Commitments from Fully Malicious PUFs](https://eprint.iacr.org/2021/248)

## New PUFs
* [Self-assembled physical unclonable function labels based on plasmonic coupling
](https://arxiv.org/abs/2310.19587)
* https://pubs.aip.org/aip/sci/article/2019/29/290009/360043/Fingerprinting-silicon-chips-just-got-easier
* [Spectral sensitivity near exceptional points as a resource for hardware encryption](https://www.nature.com/articles/s41467-023-36508-x)

## Applications
### [PUF-derived IoT identities in a zero-knowledge protocol for blockchain](https://www.sciencedirect.com/science/article/abs/pii/S2542660518301124)
> In this paper, an alternative authentication approach in which an MCU generates a secret key internally is introduced, exploiting manufacturing variability as a physical unclonable function (PUF). As the key is generated by the device itself, manufacturers save the expense of a secure environment for external key generation. In production, once chips are loaded with a firmware, it is only necessary to run an internal characterization and pass on the resulting public key, mask and helper data to be stored for authentication and recovery. Further external memory access is prevented, e.g., by blowing the JTAG security fuse. As the secret key is regenerated (with the same result each time) rather than stored in non-volatile memory, it is very hard to clone and the cost of a secure element can be saved.

> The case for such IoT devices is strengthened further in combination with a distributed ledger, or blockchain. First of all, the immutability and distributed trust provided by a blockchain can make the device authentication independent of the manufacturer. Secondly, a business process implemented in chaincode that relies on IoT inputs can validate device signatures to ensure the authenticity and integrity of those inputs.

> Replacing the central database operated by a manufacturer with a blockchain makes the system independent of the manufacturer. The chaincode will still allow only the manufacturer to create new machine entries on the distributed ledger but as the ledger content is distributed to all participants (multiple manufacturers, retailers, owners, etc.) the manufacturer is relieved of administering the system and guaranteeing its availability. A central database would go offline when the manufacturer goes out of business whereas a blockchain can survive.
> 
> Given the security disadvantages of symmetric authentication schemes (keeping a database of keys to authenticate with the risk of being hacked or lost, the risk of cloning, and barriers for third-party authentication, among others) our approach instead uses public-key cryptography based on learning parity with noise (LPN) problems, and in particular zero-knowledge (ZK) protocols to further simplify the management of device public keys. The blockchain may make the public keys generated by each device available for anyone to use in their own authentication system.
> 
> As for the second aspect, even a low-cost device can prevent manipulation of its communication with a blockchain by signing its messages with our PUF-derived keys, making the proposal suitable for any resources-limited device connected to the blockchain [9]. The chain code, in turn, can also validate the device signatures to ensure data integrity and authenticity, extending the trust the blockchain provides into the IoT device.
> 
> This paper proposes using an SRAM-based PUF to generate cryptographic keys that are employed in a zero-knowledge proof to authenticate an IoT device. We present an efficient implementation in an MCU and show that even low-cost devices can perform the required computational tasks sufficiently fast. Experimental results demonstrate that our approach is robust against temperature variations and that collisions of device identities are unlikely.

### [A survey on physical unclonable function (PUF)-based security solutions for Internet of Things](https://www.sciencedirect.com/science/article/pii/S1389128620312275)

## Commercial PUFs
https://www.cryptoquantique.com/products/qdid/

## Concerns/Questions
As per [Physical unclonable functions](https://www.nature.com/articles/s41928-020-0372-5):

> Authentication can also be executed remotely, once the CRP (challenge–response pair) is recorded in a secure database only known by the trusted party (server).

This seems to be relating to what is called remote attestation in the context of popular TEEs like SGX. In the context of SGX, for instance, the chip manufacturer is considered to be a trusted party, for various reasons (e.g: https://github.com/sbellem/qtee/issues/2).

## Hacking & Cryptanalysis
* https://github.com/nils-wisiol/pypuf (cryptanalysis)
* https://asvin.io/physically-unclonable-function-setup/
* https://github.com/nils-wisiol/LP-PUF
* https://github.com/stnolting/fpga_puf
* https://www.crypto.ruhr-uni-bochum.de/imperia/md/crypto/kiltz/ulrich_paper_47.pdf

## Specifications in Chip Designs
* https://github.com/chipsalliance/Caliptra/blob/main/doc/Caliptra.md#future-effort-caliptra-security-subsystem
* https://github.com/chipsalliance/caliptra-rtl/blob/main/docs/CaliptraIntegrationSpecification.md

## References
* [Physical One-Way Functions](https://www.science.org/doi/full/10.1126/science.1074376) _by Pappu et al._
* [On the Foundations of Physical Unclonable Functions](https://eprint.iacr.org/2009/277) _by Rührmair et al._
* [Security based on Physical Unclonability and Disorder](https://aceslab.org/sites/default/files/04-fk-PUF.pdf) _by Rührmair et al._
* [SIMPL Systems: On a Public Key Variant of Physical Unclonable Functions](https://eprint.iacr.org/2009/255) _by Rührmair_
* [Towards Secret-Free Security](https://eprint.iacr.org/2019/388.pdf) by Ruhrmair
* [Physically Unclonable Functions: A Study on the State of the Art and Future Research Directions](https://link.springer.com/chapter/10.1007/978-3-642-14452-3_1) _by Roel Maes & Ingrid Verbauwhede_
* [Silicon Physical Random Functions](https://dl.acm.org/doi/pdf/10.1145/586110.586132) _by Gassend et al._
* [PUF Taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy)

## Other References
* [Physical Unclonable Functions for Device Authentication and Secret Key Generation](https://people.csail.mit.edu/devadas/pubs/puf-dac07.pdf)
* [Feasibility and Infeasibility of Secure Computation with Malicious PUFs](https://eprint.iacr.org/2015/405)
* [Providing Root of Trust for ARM TrustZone using On-Chip SRAM](https://eprint.iacr.org/2014/464)
* [Making sense of PUFs](https://semiengineering.com/pufs-promise-better-security/)
* https://github.com/Tribler/tribler/issues/3064