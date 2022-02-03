# <img src="../../../images/operate.png" alt ='operate'  width="10%" > SCRATCh - DevOps - Operate Tools - Secure storage

[![SCRATCh - funded by BMBF](https://img.shields.io/badge/part%20of-SCRATCh-yellow)](https://scratch-itea3.eu/)
![SCRATCh - funded by BMBF](https://img.shields.io/badge/funded%20by-BMBF-blue)
[![ITEA3](https://img.shields.io/badge/supported%20by-ITEA3-orange)](https://www.itea3.org)

## A proof of concept of secure storage for an embedded IoT application

Secure storage (i.e., storage of data which remains non-accessible even with access to the device) is a fundamental asset in any application such as the Police Use Case in which devices can be intercepted by malicious actors. This enables developers to insert data that can not be read even if other parts of the system are compromised. This relies in hardware that puts a logical border between secure and insecure data in the device, such as dedicated cores of the CPUs or secure elements.

In SCRATCh we have provided a proof-of-concept development of a secure storage module connected to the Police Use Case. Since the implementation relies heavily on details of the target platform (ARM CPU and Operating System) and the fact that this remains a proprietary component for HI Iberia, only some details are shared in this repository.

## Rich Execution Environments vs. Trusted Execution Environments

Applications run under a usual Operating System have several layers of protection of the data contained in the deployment. This usually takes the form of privileges in access to resources or authentication to execute a program (for example, user accounts in UNIX based systems or Windows). However, if these security measures are compromised, all of the underlying data is accessible to the malicious user. These operating systems offer advanced capabilities and commonly provide a Rich Execution Environment (REE). Typical examples are Linux, Android or Windows.

A Trusted Execution Environment (TEE) is an environment for executing code in which those executing the code can have high levels of trust in the asset management of that surrounding environment because it can ignore threats from the “unknown” rest of the devicei. These are often based on advanced hardware measures in the device that runs the system. Both approaches are not exclusive: generally, the hardware is partitioned so that while the TEE is run in, for example, a dedicated core, the rest of the device hosts a feature Rich OS like Android.

## ARM TrustZone

TrustZone is an ARM technology that implements the hardware required in a SoC to enable the use of a TEE and a REE in parallel, with secure communications channels between them that enable the implementation of secure complete applications. It provides a cost-effective methodology to isolate security critical components in a system while not complicating life for the developers of all those other components that make the modern system on a chip (SoC) such a capable component. TrustZone + TEE techniques put the access control at the peripheral or memory and separate its management form system design and software not focused on security.

Its main drawback is the very limited nature of the communication channel and allocated resources for the TEE, which are often in the kilobit per second speed and less than 1MB total memory. This precludes the TEE to be a powerful computation engine and so it has to isolate very small jobs and or data quantities.

Since ARM SoCs are used in many applications, such as the LifeOnLive Android platform in which the SCRATCh Police UC is based, we selected TrustZone as our main security requirement for choosing hardware. The main requirement is to store facial features of suspect persons (using dlib facial vectors, less than 1KB per person) and to store the private part of cryptographic keys to encrypt communications with the server.

## Implementations of the TEE

When designing your application with the REE, you have a range of TEEs to choose from. These need to be fully supported by the toolchain in your platform and be able to securely boot in the device (that is, the execution of the TEE starts before the REE to minimize security threats).

During the course of SCRATCh, since we were experimenting mainly with the Nvidia Jetson Nano as the platform for the Police UC, we investigated the usage of Nvidia's preferred solution. Eventually, for reasons of availability and resources, we switched to an STM32 board based around the MP1 SoC.

### Proprietary Nvidia: Trusty

Trusty consists of a set of software components for supporting a Trusted Execution Environment (TEE) on mobile devices. TEE provides an execution environment that includes security features to ensure code and data on a device is protected. Trusty is part of the Android Open Source Project (AOSP). Trusty extends technology made available with the development of the Little Kernel (LK). LK is designed to provide OS primitives like threads and mutexes in a simple, lightweight package. Documentation on the [Trusty implementation can be found here](https://docs.nvidia.com/jetson/l4t/index.html).

Trusty relies on the ARM TrustZone technology and is available in the Jetson SBC family (Jetson TX2, Jetson Xavier) but not on the Jetson Nano. Due to this, an alternative was searched.

### Open Source: OP-TEE

OP-TEE is an open source Trusted Execution Enviroment (TEE) implementing the Arm TrustZone technology. OP-TEE has been ported to many Arm devices and platforms. Originally it was developed as a proprietary TEE solution by ST-Ericsson that later on was moved over to STMicroelectronics. You can find [OP-TEE documentation here](https://optee.readthedocs.io/en/latest/).

OP-TEE is divided in various components:

- A secure privileged layer, executing at Arm secure PL-1 (v7-A) or EL-1 (v8-A) level.
- A set of secure user space libraries designed for Trusted Applications needs.
- A Linux kernel TEE framework and driver (merged to the official tree in v4.12).
- A Linux user space library designed upon the GlobalPlatform TEE Client API specifications.
- A Linux user space supplicant daemon (tee-supplicant) responsible for remote services expected by the TEE OS.
- A test suite (xtest), for doing regression testing and testing the consistency of the API implementations.
- An example git containing a couple of simple host- and TA-examples.
- And some build scripts, debugging tools to ease its integration and the development of Trusted Applications and secure services.

OP-TEE is [freely available on Github](https://github.com/OP-TEE/optee_os) and has been ported to many ARM TrustZone enabled devices.

## Details of the proof of concept in SCRATCh

According to research performed during SCRATCh, it was impossible to unify the requirements of the Police UC (Linux as a REE, high performance in video processing) with the usage of any of the proposed TEE alternatives, so the development of both areas of the demonstrator was forked for different hardware platforms.

- The high performance facial matching engine was implemented in Linux on a Nvidia Jetson Nano board with 4GB RAM.
- The secure storage was implemented with OP-TEE running on a STM32MP157c-ev1 evaluation board that was too slow to perform the matching and analysis stages. The secure storage is able to store, retrieve and compare facial vectors computed by the high-performance board.

The integration of both approaches is out of scope for the SCRATCh project.
