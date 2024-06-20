---
type: slide
slideOptions:
  theme: solarized
  transition: 'fade'
---

# `qtee`

Moving Towards

**`Open Source`**

&

**`Verifiable`**

**`Secure-through-Physics`**

**TEE Chips**

_Bolton Bailey, Sam Breckenridge, Sylvain Bellemare_

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

## Current TEEs are only secure through economics

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

## SRAM PUF

<img src="https://hackmd.io/_uploads/B1qBRo3BR.png" width="750"/>

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
