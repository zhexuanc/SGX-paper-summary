# Ryoan: A Distributed Sandbox for Untrusted Computation on Secret Data
###### Tyler Hunt, Zhiting Zhu, Yuanzhong Xu, Simon Peter, Emmett Witchel

**What's the problem?**
* In multi-tenant environments, Linux container's weaker isolation guarantees, enforced through software kernel mechanisms, make it easier for attackers to compromise the confidentiality and integrity of application data within containers.

**Summary**
* Describe SCONE, a secure container mechanism for Docker that uses the SGX trusted execution support of Intel CPUs to protect container processes from outside attacks. SCONE offers a secure C standard library interface that transparently encrypts/decrypts I/O data; to reduce the performance impact of thread synchronization and system calls within SGX enclaves, SCONE supports user-level threading and asynchronous system calls.

**Key insight**
* The design of a secure container mechanism using SGX raises two challenges: (i) minimizing the size of the trusted computing base (TCB) inside an enclave while supporting existing applications in secure containers; and (ii) maintaining a low performance overhead for secure containers, given the restrictions of SGX.

**Notable design details**
* SCONE exposes an external interface based on system calls to the host OS, which is shielded from attacks. To protect the integrity and confidentiality of data processed via file descriptors, SCONE supports transparent encryption and authentication of data through shields.
* SCONE implements M:N threading to avoid the cost of unnecessary enclave translations.
* SCONE offers container processes an asynchronous system call interface to the host OS. Hence, the threads inside the enclave do not have to exit when performing system calls.

**Limitation**
* Intel SGX limitations still exists on SCONE, because the experimental evaluation of SCONE is built on SGX hardware.

**Summary of the key results**
* SCONE increases the confidentiality and integrity of containerized services using Intel SGX. The secure containers of SCONE feature a TCB of only 0.6–2 times the application code size and are compatible with Docker. Using asynchronous system calls and a kernel module, SGX-imposed enclave transition overheads are reduced effectively.
* At the same time, SCONE does not require changes to applications or the Linux kernel besides static recompilation of the application and the loading of a kernel module.

**Open questions**
* Other similar container like FlexSC batches system calls, reducing user/kernel transitions. In SCONE, application threads place system calls into a shared queue instead, which permits the OS threads to switch to other threads and stay inside the enclave, which fulfill asychronous system calls.
