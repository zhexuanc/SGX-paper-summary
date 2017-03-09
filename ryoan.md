# Ryoan: A Distributed Sandbox for Untrusted Computation on Secret Data
###### Tyler Hunt, Zhiting Zhu, Yuanzhong Xu, Simon Peter, Emmett Witchel

**What's the problem?**
* Users of modern data-processing services such as tax preparation or genomic screening are forced to trust them with data that the users wish to keep secret. Accomplishing this goal in a distributed setting is difficult because the user has no control over the service providers or the computational platform. Confining code to prevent it from leaking secrets is notoriously difficult.

**Summary**
* Ryoan provides a distributed sandbox, leveraging hardware enclaves (Intel SGX) to protect sandbox instances from potentially malicious computing platforms. The protected sandbox instances confine untrusted data-processing modules to prevent leakage of the user’s input data. Ryoan is designed for a request-oriented data model, where confined modules only process input once and do not persist state about the input.

**Key insight**
* Ryoan has a new hardware primitive that uses trusted hardware to protect a user-level computation from potentially malicious privileged software. The processor hardware keeps unencrypted data on chip, but encrypts data when it moves into RAM. The hypervisor and operating system retain their ability to manage memory, but privileged software sees only an encrypted version of the data that is protected from tampering by a cryptographic hash. 

**Notable design details**
* Ryoan adapts previous label-based systems to enable multiple mutually distrustful modules to cooperate on sensitive data. Ryoan uses secrecy labels to mark secret data and enclaves which have seen that secret data.
* Ryoan's confined environment's most important service is an in-memory virtual file system. For each unit of work, a module calls wait for work (a system service implemented by Ryoan), and the Ryoan instance reads its entire input from all input channels into memory buffers before returning to the module. 

**Limitation**
* Intel SGX hardware security limitations still exists on Ryoan, such as SGX page fault, cache timing, address bus monitoring and processor monitoring.

**Summary of the key results**
* Ryoan allows users to safely process their secret data with software they do not trust, executing on a platform they do not control, thereby benefiting users, data processing services, and computational platforms.
* Ryoan’s checkpoint-based reset is much more efficient than DSPAM and ClamAV, and the per-unit cost is under 10ms.

**Open questions**
* A company can use Ryoan to outsource email filtering and scanning while keeping email text secret. Also, Ryoan can be used in personal health analysis and image processing. What's more, a company uses Ryoan to provide a machine translation service while keeping the uploaded text secret.
