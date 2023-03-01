# qtee
Repository to explore the physical limits of trusted hardware in the classical and quantum settings.

> **Warning**: This repository may never reach its final form, and may best be viewed as an asynchronous intergalactic brainstorming time-space independent session.
>
> Said differently: [Here be dragons](https://en.wikipedia.org/wiki/Here_be_dragons) 🐉.

## Intuition
The current leading intuition of the feeble mind of this repo's author is that trusted hardware (which can withstand physical attacks) is impossible in the classical setting, meaning that an adversary who can physically access the chip will be capable to break its security because of physics, regardless of whether the chip is perfectly designed, architected, manufactured, or of whether the manufacturer is honest etc. The claim or intuition is that as per our understanding of the laws of physics, an attacker will be able to read the secret information that has been encoded into the chip and therefore will break the security of the chip. If that claim or intuition holds, then what does that mean for trusted hardware? Is it a pipe dream? Can the quantum setting make a difference? Naively thinking, what if we "throw" the secret information into a black hole? Would that help? Could a chip be designed such that it uses [nano black holes](https://en.wikipedia.org/wiki/Micro_black_hole) to store secret keys? How would key derivation work if the root keys are in a black hole? ETC.

## What's the Problem?
It may be helpful to first define what is meant by trusted hardware and more importantly what is the problem that trusted hardware aims to solve. In order to do so, we'll use the paper [Intel SGX Explained](https://eprint.iacr.org/2016/086) by _Victor Costan and Srinivas Devadas_, as it is an invaluable resource in explaining the various components of Intel SGX, which is arguably the most well-known and popular trusted hardware at the moment of this writing.

Victor Costan and Srinivas Devadas set the stage like so:

> Secure remote computation (Figure 1) is the problem of executing software on a remote computer owned and
maintained by an untrusted party, with some integrity and confidentiality guarantees. In the general setting,
secure remote computation is an unsolved problem. Fully Homomorphic Encryption [61] solves the problem for a
limited family of computations, but has an impractical performance overhead [140].
>
> Intel’s Software Guard Extensions (SGX) is the latest iteration in a long line of trusted computing (Figure 2)
designs, which aim to solve the secure remote computation problem by leveraging trusted hardware in the remote computer. The trusted hardware establishes a secure container, and the remote computation service user uploads the desired computation and data into the secure container. The trusted hardware protects the data’s confidentiality and integrity while the computation is being performed on it.

## Resources
* [Intel SGX Explained](https://eprint.iacr.org/2016/086) by _Victor Costan and Srinivas Devadas_
* [The Laws of Physics and Cryptographic Security](https://arxiv.org/abs/quant-ph/0202143) by _Terry Rudolph_
* [Is the security of quantum cryptography guaranteed by the laws of physics?](https://arxiv.org/abs/1803.04520) by _Daniel J. Bernstein_
* [Black-Hole Radiation Decoding is Quantum Cryptography](https://arxiv.org/abs/2211.05491) by _Zvika Brakerski_ (Thanks to [@tyurek](https://github.com/tyurek) for sharing)
* [On black holes, holography, the Quantum Extended Church-Turing Thesis, fully homomorphic encryption, and brain uploading](https://scottaaronson.blog/?p=6599) by _Scott Aaronson_
* [Hayden–Preskill thought experiment](https://en.wikipedia.org/wiki/Hayden%E2%80%93Preskill_thought_experiment)
* [Here’s one way to get out of a black hole!](https://quantumfrontiers.com/2017/04/03/heres-one-way-to-get-out-of-a-black-hole/) by _John Preskill_
* [Using Memory Errors to Attack a Virtual Machine](https://www.cs.princeton.edu/~appel/papers/memerr.pdf) by _Sudhakar Govindavajhala and Andrew W. Appel_ (thanks to [@intoverflow](https://github.com/intoverflow) for sharing)
* [A2: Analog Malicious Hardware](http://static1.1.sqspcdn.com/static/f/543048/26931843/1464016046717/A2_SP_2016.pdf) by _Kaiyuan Yang, Matthew Hicks, Qing Dong, Todd Austin, Dennis Sylvester_ (thanks to [@intoverflow](https://github.com/intoverflow) for sharing)
* https://quantumfrontiers.com/author/preskill/

### About Black Holes
* [Search for microscopic black hole signatures at the large hadron collider](https://cms.cern/news/search-microscopic-black-hole-signatures-large-hadron-collider)
* [Micro black hole](https://en.wikipedia.org/wiki/Micro_black_hole)
* [Extra dimensions, gravitons, and tiny black holes](https://home.cern/science/physics/extra-dimensions-gravitons-and-tiny-black-holes)
* [Mini Black Holes Easier To Make Than Thought](https://www.livescience.com/27811-creating-mini-black-holes.html)
* [Information encoded on the surface of a black hole](https://physics.stackexchange.com/questions/17338/information-encoded-on-the-surface-of-a-black-hole)
* [A spiderweb of wormholes could solve a fundamental paradox first proposed by Stephen Hawking](https://www.livescience.com/black-hole-paradox-solution)
* [Black hole information paradox](https://en.wikipedia.org/wiki/Black_hole_information_paradox)
* [Black Hole Encryption](https://www.science.org/doi/10.1126/science.311.5767.1525a)
* [Hayden-Preskill thought experiment](https://youtu.be/lV1ePoCeOdQ)

### PUFs: Physical Unclonable Functions
* Nature Electronics: https://www.nature.com/articles/s41928-020-0372-5?proof=t
* Wikipedia: https://en.wikipedia.org/wiki/Physical_unclonable_function

* [On the Physical Security of Physically Unclonable Functions](https://d-nb.info/1156184150/34Security%20Analysis%20of%20Physically%20Unclonable%20Functions%20against%20Physical%20Attacks)
* [A Fourier Analysis Based Attack against Physically Unclonable Functions](https://eprint.iacr.org/2017/551.pdf)



## Contributing
Please do! File issues & pull requests as you wish!. Don't hold back!

Loosely will attempt to follow the [ZeroMQ RFC 42/C4: Collective Code Construction Contract](https://rfc.zeromq.org/spec/42/).

But don't worry about it! Just write your mind in the form of issues and pull requests!
