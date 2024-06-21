---
type: slide
slideOptions:
  theme: solarized
  transition: 'fade'
---

# `qtee`

Moving Towards

**`Open Source`** & **`Verifiable`**

**`Secure-through-Physics`**

**TEE Chips**

_Bolton Bailey, Sam Breckenridge, Sylvain Bellemare_

IC3 2024 Blockchain Camp

---

# The Problem

> Secure remote computation is the problem of executing software on a remote computer **owned and maintained by an untrusted party**, with some integrity and confidentiality guarantees.
> -- [Intel SGX Explained](https://eprint.iacr.org/2016/086), Devadas

---

Intel SGX aims to solve the secure remote computation problem with hardware.

---

## 3 core challenges of TEEs

* **NO proof of non-leakage of root of trust**

* **NO proof of manufacturing**

* **Centralized remote attestation**

---

## Current TEEs are ultimately secure through economics

---

> TEEs running in the cloud would need the cloud provider and Intel to collude, making such an attack even less likely.
> -- [Debunking TEE FUD: A Brief Defense of The Use of TEEs in Crypto](https://collective.flashbots.net/t/debunking-tee-fud-a-brief-defense-of-the-use-of-tees-in-crypto/2931), Quintus & Miller

---

<img src="https://hackmd.io/_uploads/SknpIkhSA.png" height="680" width="2300"/>
<!--
<img style="float: right" src="https://hackmd.io/_uploads/SknpIkhSA.png" width="2000"/>
-->

---

<span>SGX Threat Model<!-- .element: class="fragment" data-fragment-index="1" highlight-red --></span>

<span>No physical attacks (targeting the CPU chip)<!-- .element: class="fragment" data-fragment-index="2" --></span>

<span>No side-channel attacks<!-- .element: class="fragment" data-fragment-index="3" -->
</span>



<!-- .slide: data-background="https://hackmd.io/_uploads/H1J-I32rA.png" data-background-size="680px" -->

---

![image](https://hackmd.io/_uploads/BJx-D23HA.png)

---

# But. Why?

---

<!-- .slide: style="font-size: 32px;" -->

> **_Information is not a disembodied abstract entity; it is always tied to a physical representation. It is represented by engraving on a stone tablet, a spin, a charge,
a hole in a punched card, a mark on paper, or some other equivalent._** _This ties the handling of information to all the possibilities and restrictions of our real physical word, its laws of physics and its storehouse of available parts._
>
> -- **Rolf Landauer**, in The physical nature of information

---

<!-- .slide: style="font-size: 16px;" -->

# - External Root of Trust - | - Internal Root of Trust -

![image](https://hackmd.io/_uploads/ryMqEkhS0.png)

Image source: [Root of Trust](https://www.synopsys.com/dw/doc.php/wp/gsa-end-to-end-traceability-of-ip-wp.pdf), _by Vincent Van der Leest et al_

---

<!-- .slide: style="font-size: 16px;" -->

<img src="https://hackmd.io/_uploads/r1d9Ol3BA.png" />

slide by [Ulrich Rührmair](https://youtu.be/oditVzrFa34?si=w92fUc1h7YNJBQYM)

---

<!-- .slide: style="font-size: 16px;" -->

<img src="https://hackmd.io/_uploads/S1NZ7xhBC.png" width="800"/>

slide by [Ulrich Rührmair](https://youtu.be/oditVzrFa34?si=w92fUc1h7YNJBQYM)

---

## Physical One-Way Functions

![image](https://hackmd.io/_uploads/S1pmMxhH0.png)

_[Pappu et al.](https://www.science.org/doi/full/10.1126/science.1074376)_

---

## The Rise of Crypto-Physics
**Physical One-Way Functions**
-- [PhD thesis](https://dspace.mit.edu/handle/1721.1/45499) by Pappu

> "Our work is philosophically inspired by the notion of Quantum Money, first proposed in 1983 by Wiesner in a paper titled [Conjugate Coding](https://dl.acm.org/doi/10.1145/1008908.1008920)".


<!-- In this paper, Wiesner presented two ideas. The first one was a verify-only memory, that, with high probability, cannot be read or copied by someone ignorant of its contents. The second idea was a scheme to multiplex two messages in such a way that, with high probability, either message could be recovered at the cost of irreversibly destroying the other.
-->


<!--
<img src="https://hackmd.io/_uploads/H1bb_lhHC.png" />
-->

---

<!-- .slide: style="font-size: 28px;" -->

## SRAM PUF

<img src="https://hackmd.io/_uploads/B1qBRo3BR.png" width="750"/>

source: [Physical Unclonable Functions and Applications: A Tutorial](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6823677)

* Weak PUF
* Attacks -> Data remanence, semi-invasive

---

## Arbiter PUF
![image](https://hackmd.io/_uploads/HyB9C1e8R.png)

source: [Physical Characterization of Arbiter PUFs](https://eprint.iacr.org/2014/802)

* Vulnerable to semi-invasive attacks?
* Serialized = 1 response at a time

<!--
<img src="https://hackmd.io/_uploads/BkPi4l3B0.png" width="700"/>


slide by [Ulrich Rührmair](https://youtu.be/oditVzrFa34?si=w92fUc1h7YNJBQYM)
-->

---

# `zeepuf`
* TEE based on [Keystone Enclave](https://github.com/keystone-enclave/keystone) and [SIMPL PUF](https://eprint.iacr.org/2009/255.pdf)
* **Highly theoretical & hypothetical**
* **Probably would NOT work**
* Goal: **SPARK** exploration of open source TEEs

---

<!-- .slide: style="font-size: 16px;" -->

# Keystone Arch Overview
![image](https://hackmd.io/_uploads/rJWsUtcHR.png)

Image source: [Keystone Enclave Documentation](https://docs.keystone-enclave.org/en/latest/Getting-Started/How-Keystone-Works/Keystone-Basics.html)


---

<!-- .slide: style="font-size: 16px;" -->

<img src="https://hackmd.io/_uploads/BkyCBxnrR.png" width="800"/>

slide by [Ulrich Rührmair](https://youtu.be/oditVzrFa34?si=w92fUc1h7YNJBQYM)

---

<!-- #### SIMPL: key-free PUF -->

<img src="https://hackmd.io/_uploads/S1cR5qoH0.png" width="700"/>

Image source: [SIMPL System](https://eprint.iacr.org/2009/255.pdf), by Rührmair


* Physical system $\rightarrow S$
* Description of $S \rightarrow D(S)$
* Simulation algorithm $\rightarrow \tt{Sim}$
* Set of possible challenges $\rightarrow \bf{C}$

---

# Remote Attestation with `zeepuf`

---

## Cast of Characters

* **Alice**, the **prover** - owns a **`zeepuf`** machine; executes computations as a service. MUST prove that the computations are done with authentic zeepuf hardware, and with the enclave application, provided by Bob, the verifier
* **Bob**, the **verifier** - outsources a computation, in the form of an enclave application binary, to Alice, the prover, whom he does not trust

---

<!-- .slide: style="font-size: 16px;" -->

# Keystone Workflow

<img src="https://hackmd.io/_uploads/rkuqCY9HA.png" width="850"/>

Image source: [Keystone Enclave Documentation](https://docs.keystone-enclave.org/en/latest/Getting-Started/How-Keystone-Works/Keystone-Basics.html)

---

<!-- .slide: style="font-size: 16px;" -->

# Keystone Remote Attestation
![image](https://hackmd.io/_uploads/SJBeJq5HA.png)

Image source: [Keystone Enclave Documentation](https://docs.keystone-enclave.org/en/latest/Getting-Started/How-Keystone-Works/Keystone-Basics.html)


---

### Elements of the Remote Attestation Flow
<!-- .slide: style="text-align: left" -->

* Secure Monitor Hash: $\color{forestgreen}{M_H = H(M)}$
* Enclave App Hash: $\color{forestgreen}{E_H = H(E)}$
* Attestation Payload: $\color{forestgreen}{A = H(M_H, E_H)}$

Bob knows $\color{forestgreen}{M_H}$ and $\color{forestgreen}{E_H}$.
Alice MUST prove that she's using the expected secure monitor and enclave app, by sending an attestation payload.

---

Alice, owner of a `zeepuf` machine, $\color{forestgreen}{S}$, proves to Bob that she is running a legit Keystone enclave app $\color{forestgreen}{E}$.

Alice has put $\color{forestgreen}{D(S), \tt{Sim}, t_{max}, \textbf{C}}$ on a public blockchain, perhaps after a cut-and-choose "verification" process ([1](https://link.springer.com/referenceworkentry/10.1007/0-387-23483-7_92), [2](https://github.com/sbellem/qtee/issues/2#issuecomment-1464600086), [3](https://eprint.iacr.org/2022/1720.pdf)).

Now, she can prove to Bob that she is executing the expected keystone app, represented by $\color{forestgreen}{E}$ to Bob as follows.

---

# Protocol
_Based on [SIMPL System](https://eprint.iacr.org/2009/255.pdf), section 4.2, by Rührmair_

---

1. Bob reads $\color{forestgreen}{D(S), \tt{Sim}, t_{max}, \textbf{C}}$ associated with Alice from the blockchain

2. Bob sends a number of randomly chosen challenges $\color{forestgreen}{C_1, \ldots , C_k \in \textbf{C}}$ to Alice

3. Alice uses $\color{forestgreen}{S}$ to determine the corresponding values $\color{forestgreen}{R_1, \ldots, R_k}$. She derives $\color{forestgreen}{l}$ keys $\color{forestgreen}{K_1, \ldots, K_l}$ from these values, with a public hash function.

4. Alice computes the attestation payload, $\color{forestgreen}{A = H(M_H, E_H)}$ -- (hash of secure monitor + enclave binary loaded in `zeepuf`)

---

5. Alice uses a $\color{forestgreen}{\tt{MAC}}$ with $\color{forestgreen}{K_1, \ldots, K_l}$, and sends the values $\color{forestgreen}{A, {\tt{MAC}}_{K_1}(A), \ldots, {\tt{MAC}}_{K_l}(A)}$ to Bob

6. Bob gets $\color{forestgreen}{A', V_1, \ldots , V_l}$; measures $\color{forestgreen}{\Delta t}$ between sending the $\color{forestgreen}{C_1, \ldots, C_k}$ in step 2 and receiving $\color{forestgreen}{A', V_1, \ldots, V_l}$. If $\color{forestgreen}{\Delta t \gt 2 \cdot t_{max}}$, then abort

7. Bob computes the values $\color{forestgreen}{R_1, \ldots, R_k}$ by simulation via $\color{forestgreen}{\tt{Sim}}$, and derives the keys $\color{forestgreen}{K'_1, \ldots, K'_l}$ by application of the same hash function as in step 3

---

8. Bob checks if for all $\color{forestgreen}{i = 1, \ldots, l}$, $$\color{forestgreen}{{\tt{MAC}}_{K'_i}(A') = V_i.}$$ If true, then Bob trusts $\color{forestgreen}{A' = A}$
 
9. If properly authenticated, Bob checks that $\color{forestgreen}{A' = H(M'_H, E'_H)}$. If the resulting hash matches, then Bob can trust that Alice is using the expected software 


---

# Discussion

---

## Future Work & Directions

* Proof of Manufacturing (cut-and-choose)
* Real-world implementation: SRAM PUFs
* Open source SRAM PUFs?
* Attacks on SRAM PUFs (helper data, error correction)
* Keystone + sanctum (drawback with honest but curious manufacturer)
* Optimizations on SIMPL PUF (VDF + SNARK)
* Blogpost in the works
* See 

---

## Proof of Manufacturing

* Open source Hardware Design
* Use Google Skywater or others for fab
* [Use SEM to verify chips against open source hardware design](https://eprint.iacr.org/2022/1720.pdf) with [Cut-and-Choose](https://github.com/sbellem/qtee/issues/2#issuecomment-1464600086) approach
* Supply-chain on a blockchain

---

<!-- .slide: style="font-size: 16px;" -->

# Blockchain & PUF -based trusted supply chain

![image](https://hackmd.io/_uploads/B1nJBJ2SR.png)

Image source: [Root of Trust](https://www.synopsys.com/dw/doc.php/wp/gsa-end-to-end-traceability-of-ip-wp.pdf), _by Vincent 
Van der Leest et al_

---

### A note about Cloud based envs
[Remote inspection of adversary-controlled environments](https://www.nature.com/articles/s41467-023-42314-2.pdf)

---

### PUF Attacks

* [Physical Characterization of Arbiter PUFs](https://eprint.iacr.org/2014/802)

---

<!-- .slide: style="font-size: 36px;" -->

## PUFs' Curated List of Readings
* [Physical One-Way Functions](https://www.science.org/doi/full/10.1126/science.1074376) _by Pappu et al._
* [Physically Unclonable Functions: A Study on the State of the Art and Future Research Directions](https://link.springer.com/chapter/10.1007/978-3-642-14452-3_1) _by Roel Maes & Ingrid Verbauwhede_
* [On the Foundations of Physical Unclonable Functions](https://eprint.iacr.org/2009/277) _by Rührmair et al._
* [Security based on Physical Unclonability and Disorder](https://aceslab.org/sites/default/files/04-fk-PUF.pdf) _by Rührmair et al._
* [SIMPL Systems: On a Public Key Variant of Physical Unclonable Functions](https://eprint.iacr.org/2009/255) _by Rührmair_
* [Towards Secret-Free Security](https://eprint.iacr.org/2019/388.pdf) by Ruhrmair
* [PUF Taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy)

---

# Acknowledgments
Pratyush Ranjan Tiwari (Johns Hopkins)
Thorben Moos (UCLouvain, Belgium)
Francois-Xavier Standaert (UCLouvain, Belgium)

---

## References

<!-- .slide: style="font-size: 24px;" -->

* [SIMPL System: On a Public Key Variant of Physical Unclonable Functions](https://eprint.iacr.org/2009/255.pdf), Ulrich Rührmair
* [Red Team vs. Blue Team: A Real-World Hardware Trojan Detection Case Study Across Four Modern CMOS Technology Generations](https://eprint.iacr.org/2022/1720), by Puschner et al

---

# PUFs Reloaded

An extended exploration of PUFs

---

<!-- .slide: style="font-size: 32px;" -->

### Commercial PUFS
**Mechanism**: Electronic | **Implicity**: Implicit | **Evaluation**: Intrinsic

<table>
  <thead>
    <tr>
      <th>Concept</th>
      <th>Parameter</th>
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
      <td rowspan=1>Time</td>
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
  </tbody>
</table>

Partial table source: [A PUF taxonomy](https://pubs.aip.org/aip/apr/article/6/1/011303/571003/A-PUF-taxonomy) by McGrath et al.

---

<a href="https://github.com/sbellem/qtee/blob/zeepuf/zeepuf-slides.md">
<svg xmlns="http://www.w3.org/2000/svg" height="256" width="248" viewBox="0 0 496 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.--><path fill="#63E6BE" d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3 .3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5 .3-6.2 2.3zm44.2-1.7c-2.9 .7-4.9 2.6-4.6 4.9 .3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3 .7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3 .3 2.9 2.3 3.9 1.6 1 3.6 .7 4.3-.7 .7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3 .7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3 .7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"/></svg></a>

<!--
[hackmd](https://hackmd.io/0zpr6jNiQgOkKaipSl2pHw)
-->

---

<!---
### References

* Open Fabs: https://wiki.f-si.org
* SEM verification: https://eprint.iacr.org/2022/1720.pdf
* Cut-and-Choose Scheme: https://github.com/sbellem/qtee/issues/2#issuecomment-1464600086


# Into the Future

### Combine PUF with VDF

### PUFcoin

### Quantum One-Shot Signatures

### Quantum TEEs

### Nano Black Holes

--->
