
<!--
## [`Here Come The Pufpunks`](https://youtu.be/YE0QqNAMbAA?si=LVfwr-KK7RLdhmqa)
-->

<a href="https://youtu.be/YE0QqNAMbAA?si=LVfwr-KK7RLdhmqa"><span style="font-weight: bold; font-size: 61pt; color:green">Here Come The Pufpunks<!-- .element: class="fragment" data-fragment-index="0" --></span></a>

<span style="font-weight: bold; font-size: 32pt; color:yellow">Marching Towards<!-- .element: class="fragment" data-fragment-index="1" --></span>

<span style="font-weight: bold; font-size: 36pt; color:yellow">Open Source & Verifiable<!-- .element: class="fragment" data-fragment-index="2" --></span>
    
<span style="font-weight: bold; font-size: 36pt; color:yellow">Secure-through-Physics<!-- .element: class="fragment" data-fragment-index="3" --></span>

<span style="font-weight: bold; font-size: 36pt; color:yellow">PUF-based TEEs<!-- .element: class="fragment" data-fragment-index="4" --></span>

<a href="https://lu.ma/tee.salon"><span style="font-weight: bold; font-size: 24pt; color:orange">Flashbots TEE.Salon @ EthCC Brussels 2024<!-- .element: class="fragment" data-fragment-index="5" --></span></a>

<a href="https://www.initc3.org/"><span style="font-weight: bold; font-size: 24pt; color:green">Sylvain Bellemare, IC3 (Cornell)<!-- .element: class="fragment" data-fragment-index="6" --></span></a>

<!--
![image](https://hackmd.io/_uploads/BkI36S6wC.png)
-->


<!-- .slide: data-background="https://hackmd.io/_uploads/BkI36S6wC.png" data-background-size="2100px" -->

---

# [The Problem](https://hackmd.io/@sbellem/qtee#The-Problem-TEEs-aim-to-solve)

> Secure remote computation is the problem of executing software on a remote computer **owned and maintained by an untrusted party**, with some integrity and confidentiality guarantees.
> -- [Intel SGX Explained](https://eprint.iacr.org/2016/086), Devadas

---

Intel SGX aims to solve the secure remote computation problem with hardware.

---

## [3 core challenges of TEEs](https://hackmd.io/@sbellem/qtee#Four-Core-Challenges-for-TEEs)

* **NO proof of non-leakage of root of trust**

* **NO proof of manufacturing**

* **Centralized remote attestation**

---

## [Current TEEs are ultimately secure through economics](https://hackmd.io/@sbellem/qtee#Motivation)

---

> TEEs running in the cloud would need the cloud provider and Intel to collude, making such an attack even less likely.
> -- [Debunking TEE FUD: A Brief Defense of The Use of TEEs in Crypto](https://collective.flashbots.net/t/debunking-tee-fud-a-brief-defense-of-the-use-of-tees-in-crypto/2931), Quintus & Andrew

---

<img src="https://hackmd.io/_uploads/SknpIkhSA.png" height="680" width="2300"/>
<!--
<img style="float: right" src="https://hackmd.io/_uploads/SknpIkhSA.png" width="2000"/>
-->

---

<a href="https://eprint.iacr.org/2016/086">
<span style="font-weight: bold; color:red; font-size: 60pt">SGX Threat Model<!-- .element: class="fragment" data-fragment-index="1" highlight-red --></span>
</a>

<span style="font-weight: bold; color: red; font-size: 34pt">No physical attacks (targeting the CPU chip)<!-- .element: class="fragment" data-fragment-index="2" --></span>

<span style="font-weight: bold; color: red; font-size: 34pt">No side-channel attacks<!-- .element: class="fragment" data-fragment-index="3" -->
</span>



<!-- .slide: data-background="https://hackmd.io/_uploads/H1J-I32rA.png" data-background-size="680px" -->

---

[![image](https://hackmd.io/_uploads/BJx-D23HA.png)](https://youtu.be/otCpCn0l4Wo?si=yBrxVUsHPcmWC3NZ)

---

# But. Why?

---

<!-- .slide: style="font-size: 32px;" -->

> **_Information is not a disembodied abstract entity; it is always tied to a physical representation. It is represented by engraving on a stone tablet, a spin, a charge,
a hole in a punched card, a mark on paper, or some other equivalent._** _This ties the handling of information to all the possibilities and restrictions of our real physical word, its laws of physics and its storehouse of available parts._
>
> -- **Rolf Landauer**, in [The physical nature of information](https://cqi.inf.usi.ch/qic/64_Landauer_The_physical_nature_of_information.pdf)

---

## How do you hide bits & atoms?

---

## Euh ... put them in a black hole?

---

## [Black-Hole Radiation Decoding](https://arxiv.org/abs/2211.05491) 
### [is](https://arxiv.org/abs/2211.05491)
## [Quantum Cryptography](https://arxiv.org/abs/2211.05491)

-- _Zvika Brakerski_

---

## [I'm afraid of Schrödinger's cat](https://en.wikipedia.org/wiki/Schr%C3%B6dinger%27s_cat?)

\begin{equation}
i\hbar \frac{\partial \Psi(\mathbf{r}, t)}{\partial t} = \hat{H} \Psi(\mathbf{r}, t)
\end{equation}


---

# [Enter PUF Land](https://youtu.be/_W7wqQwa-TU?si=KAbcSIHV5B666Jgp)

<!--
<img src="https://hackmd.io/_uploads/SkEQpG9UC.png" width="130">
-->

---

## [The Rise of CryptoPhysics](https://hackmd.io/@sbellem/qtee#The-Rise-of-Crypto-Physics)

[**Physical One-Way Functions**](https://dspace.mit.edu/handle/1721.1/45499)
-- PhD thesis by Pappu

> "Our work is philosophically inspired by the notion of **Quantum Money**, first proposed in 1983 by Wiesner in a paper titled [Conjugate Coding](https://dl.acm.org/doi/10.1145/1008908.1008920)."


<!-- In this paper, Wiesner presented two ideas. The first one was a verify-only memory, that, with high probability, cannot be read or copied by someone ignorant of its contents. The second idea was a scheme to multiplex two messages in such a way that, with high probability, either message could be recovered at the cost of irreversibly destroying the other.
-->


<!--
<img src="https://hackmd.io/_uploads/H1bb_lhHC.png" />
-->

---

## [Physical One-Way Functions]((https://www.science.org/doi/full/10.1126/science.1074376))

<!-- ![image](https://hackmd.io/_uploads/S1pmMxhH0.png) -->
![image](https://hackmd.io/_uploads/HkiXMIc8R.png)

-- _Pappu et al._

---

<!-- .slide: style="font-size: 36px;" -->

## [Physical Unclonable Functions (PUFs)](https://dl.acm.org/doi/10.1145/586110.586132)

> "We wish to implement a PUF in silicon so we can **identify and authenticate** a given **integrated circuit** (IC). By exploiting **statistical variations** in the delays of devices and wires within the IC, we create a **manufacturer resistant** PUF."

-- _Gassend et al._


---

<!-- .slide: style="font-size: 16px;" -->

# Arbiter PUF
![image](https://hackmd.io/_uploads/SkwsDM9I0.png)
source: [Physically Unclonable Functions: A Study on the State of the Art and Future Research Directions](https://link.springer.com/chapter/10.1007/978-3-642-14452-3_1) _by Maes & Verbauwhede_

---

<!-- .slide: style="font-size: 36px;" -->

> "Again, the hardness of cloning can be considered from a theoretical and a practical point of view. Practically, cloning can be very hard or infeasible. Demonstrating theoretical unclonability on the other hand is very difficult. The only known systems which can be proven to be theoretically unclonable are based on quantum physics."
> 
> -- [Physically Unclonable Functions: A Study on the State of the Art and Future Research Directions](https://link.springer.com/chapter/10.1007/978-3-642-14452-3_1) _by Maes & Verbauwhede_


---

<!-- .slide: style="font-size: 16px;" -->

# - Extrinsic Security - | - Intrinsic Security -

![image](https://hackmd.io/_uploads/ryMqEkhS0.png)

Image source: [Root of Trust](https://www.synopsys.com/dw/doc.php/wp/gsa-end-to-end-traceability-of-ip-wp.pdf), _by Vincent Van der Leest et al_

---

# Discussion

---

<!-- .slide: style="font-size: 32px;" -->

# Related Work
* [The Secure Cryptographic Implementation Association](simple-crypto.org)
* [Here Come The Pufpunks](https://hackmd.io/@sbellem/qtee) (_aka qtee_)
* [Autonomous TEE Manifesto](https://poeticte.ch/posts/autonomous-TEEs-manifesto.html)
* [Flashbots' call to action](https://collective.flashbots.net/t/project-t-tee-from-trusted-to-trustless-execution-environments/3541) 

---

<!-- .slide: style="font-size: 32px;" -->

## [With A Little Help From My Friends](https://youtu.be/6waXtxosJ4A?si=4ACOpW-UylJJ7VHz)

[Thorben](https://www.thorbenmoos.de/), [UCLouvain Crypto Group](https://www-crypto.elen.ucl.ac.be/crypto/)
[François-Xavier](https://www-crypto.elen.ucl.ac.be/crypto/author/francois-xavier-standaert/), [UCLouvain Crypto Group](https://www-crypto.elen.ucl.ac.be/crypto/)
[Davie]() & [Julio](https://x.com/Julio_Linares_), [Poetic Technologies UG](https://poeticte.ch/)
[Tina](https://x.com/tzhen), [Flashbots](https://www.flashbots.net/)
[Andrew](https://x.com/socrates1024), [Initiative for Cryptocurrencies and Contracts](https://initc3.org)

<a href="https://www-crypto.elen.ucl.ac.be/crypto/">
    <img src="https://hackmd.io/_uploads/S1GOSNW_R.png"
         width="123"/>
</a>

<a href="https://poeticte.ch/">
    <img src="https://hackmd.io/_uploads/rkNk_VZdR.png"
         width="300"/>
</a>

<a href="https://www.flashbots.net/">
    <img src="https://hackmd.io/_uploads/rJGoINWuA.png"
         width="120"/>
</a>

<a href="https://initc3.org/">
    <img src="https://hackmd.io/_uploads/rJZ9ME-uR.png"
         width="500"/>
</a>


<!--

## PUFs' Curated List of Readings
* [Physical One-Way Functions](https://www.science.org/doi/full/10.1126/science.1074376) _by Pappu et al._
* [Physically Unclonable Functions: A Study on the State of the Art and Future Research Directions](https://link.springer.com/chapter/10.1007/978-3-642-14452-3_1) _by Roel Maes & Ingrid Verbauwhede_
* [On the Foundations of Physical Unclonable Functions](https://eprint.iacr.org/2009/277) _by Rührmair et al._
* [Security based on Physical Unclonability and Disorder](https://aceslab.org/sites/default/files/04-fk-PUF.pdf) _by Rührmair et al._
* [SIMPL Systems: On a Public Key Variant of Physical Unclonable Functions](https://eprint.iacr.org/2009/255) _by Rührmair_
* [Towards Secret-Free Security](https://eprint.iacr.org/2019/388.pdf) by Ruhrmair
* [PUF Taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy)
-->
