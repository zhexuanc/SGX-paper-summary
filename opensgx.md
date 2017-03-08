# OpenSGX: An Open Platform for SGX Research
Prerit Jain   Soham Desai   Seongmin Kim   Ming-Wei Shih   JaeHyuk Lee
Changho Choi   Youjung Shin  Taesoo Kim   Brent Byunghoon   Kang Dongsu Han

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
* OpenSGX is not secure for any security-related projects.
* Intel SGX has a very restricted set of the I/O channels, so that it is essential to establish a secure channel between users and the enclave program.

**Summary of the key results**
* Developing a complete platform for SGX development that includes emulated hardware and operating system components, an enclave program loader, an OpenSGX user library, and debugging and performance monitoring support.
* Our evaluation of OpenSGX demonstrates that it can run nontrivial applications, such as the Tor anonymity network, and new ideas can be easily implemented and evaluated as a proof-ofconcept using our framework.

**Open questions**
* OpenSGX can be utilized or extended for easy development of Intel SGX such as toolchains or a library, precise profiling of SGX programs and the exploration of potential research opportunities beyond the software boundary that the Intel SGX can not flexibly enable.
