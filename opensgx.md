

**What's the problem?**
* Trusted execution environment has rapidly matured over last decade, for example the Intel SGX. However, software technology lag behind the hardware part.

**Summary**
* Establish the first open platform for SGX research adn development, and it is an initial exploration of system support, interface design and the security issues involving system calls and user library for SGX programming. Also, applying OpenSGX to Tor nodes to isolate sensitive information and evaluate its potential performance implications.

**Key insight**
* Using QEMU to implement OpenSGX's OS emulation layer and hardware emulation such as SGX instructions. It provides a rich development environment allowing the research community to easily emulate a program running inside an enclave.

**Notable design details**
* OpenSGX supports instruction-level compatibility to SGX-aware binaries by implementing the core Intel SGX instructions.
* To enforce EPC access protection, OpenSGX interposes every single memory access and checks the execution context and the corresponding access permission.
* OpenSGX user library provides a dedicated communication channel between an enclave and its host.

**Limitation**
* 
