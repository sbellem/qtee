# qtee
Repository to explore the physical limits of trusted hardware in the classical and quantum settings.

It may be helpful to first define what is meant by trusted hardware and more importantly what is the problem that trusted hardware aims to solve. In order to do so, we'll use the paper [Intel SGX Explained](https://eprint.iacr.org/2016/086) by _Victor Costan and Srinivas Devadas_, as it is an invaluable resource in explaining the various components of Intel SGX, which is arguably the most well-known and popular trusted hardware at the moment of this writing.

Victor Costan and Srinivas Devadas set the stage like so:

> Secure remote computation (Figure 1) is the problem of executing software on a remote computer owned and
maintained by an untrusted party, with some integrity and confidentiality guarantees. In the general setting,
secure remote computation is an unsolved problem. Fully Homomorphic Encryption [61] solves the problem for a
limited family of computations, but has an impractical performance overhead [140].
>
> Intel’s Software Guard Extensions (SGX) is the latest iteration in a long line of trusted computing (Figure 2)
designs, which aim to solve the secure remote computation problem by leveraging trusted hardware in the remote computer. The trusted hardware establishes a secure container, and the remote computation service user uploads the desired computation and data into the secure container. The trusted hardware protects the data’s confidentiality and integrity while the computation is being performed on it.
