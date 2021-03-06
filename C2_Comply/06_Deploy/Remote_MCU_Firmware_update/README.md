# <img src="../../../images/deploy.png" alt ='deploy'  width="10%" > SCRATCh - DevOps - Deploy Tools - Remote MCU Firmware update via Git Server & Trust Provisioning Services

[![Available](https://img.shields.io/badge/status-Available-green)](https://github.com/SCRATCh-ITEA3/imxrt1060-fwupdate-via-git)
[![SCRATCh - funded by BMBF](https://img.shields.io/badge/part%20of-SCRATCh-yellow)](https://scratch-itea3.eu/)
![SCRATCh - funded by BMBF](https://img.shields.io/badge/funded%20by-BMBF-blue)
[![ITEA3](https://img.shields.io/badge/supported%20by-ITEA3-orange)](https://www.itea3.org)


# Remote MCU Firmware updates via Git Server


## Automated build & deploy pipeline for embedded targets

*Context:* The created automated cloud based build and deploy pipeline enables a developer to push the source code developed for an embedded target into an online private GitHub repository, from where the pipeline takes over to build an application image from it, secure the application image and finally deploy it to a public GitHub repository from where it can be downloaded for further deployment.
<img src="images/automated-build-chain-for-embedded-target.png" alt="automated-build-chain-for-embedded-target" style="height:90px; margin-left:50px;"/>

It leverages several tools as listed in the following:
* [NXP MCUXpresso IDE]
* [Docker] used to encapsulate MCUXPresso IDE as target aware compiler in a cloud based runner
* [GitHub Actions] Used for automation of the pipeline on GitHub
* [LPC8N04 Application notes] *TN00040* contains secure image creator tool used for securing the firmware image

## NFC based firmware update for resource constrained IoT devices 

*Context:* Tools used to show an indirect firmware update of a very resource constrained but NFC enabled MCU (ARM Cortex M0+ @8MHz, 32kB program flash memory), without direct cloud access. The update happens via an NFC capable Smartphone as intermediate that receives the secured app binary from the cloud and forwards it to the embedded device via NFC. The validation of security measures then happens on the embedded device.

<img src="images/signed-low-end-mcu-updates-via-nfc.png" alt="signed-low-end-mcu-updates-via-nfc" style="height:65px; margin-left:25px;"/>

Used tools:
* NXP firmware update demo consisting of compiled second stage bootloader for the MCU that validates firmware images and the corresponding secure_image_creator desktop tool for securing the image: [LPC8N04 Application notes]
    >*LPC8N04: Encrypted Over the Air (OTA) Firmware update using NFC - Application Note TN00040*.
* [Android Smartphone application] used to foward firwmare image from cloud towards NFC capable MCU
    > *Design Resources > SOFTWARE > Embedded Software > BSP, Drivers and Middleware > Code Snippets > LPC8N04 NFC Demo Android (LPC8N04-NFCDEMO)*
* [NXP MCUXpresso IDE]    




## TLS secured crossover MCU firmware update

The demo shows a [Git based remote firmware update of a crossover MCU]. Such microcontrollers hold as example for a typical processor in IoT or edge devices. As server to provide the updated firmware also this demo just uses an online Git server. In contrast to the previous two sections this IoT device has direct internet access via TCP/IP. The firmware download is secured through a TLS tunnel.

The idea behind is that small to medium enterprises that want to deploy IoT systems may not have the resources to afford or maintain an own IoT cloud infrastructure like AWS or Azure. Leveraging open source services like GitHub for the firmware deployment can enable these companies deploying their own IoT systems.

<img src="images/tls-secured-crossover-mcu-firmware-update.png" alt="tls-secured-crossover-mcu-firmware-update" style="height:70px; margin-left:35px;"/>

Used tools / libraries:
* [Mbed TLS]
* [lwIP]
* [NXP MCUXpresso IDE]


# Edgeverse
Both EdgeLock?? 2GO and EdgeLock?? SE050 being a part of Edgeverse platform, offer primary edge computing capabilities. This software is built on the foundation of scalability, energy efficiency, security, machine learning and connectivity. 

## EdgeLock?? 2GO
Secure and Flexible IoT service platform designed for easy, secure deployment and management of devices and services. Cost optimization can be achieved by choosing the options that are right for you using this flexible IoT device platform 

https://www.nxp.com/products/security-and-authentication/secure-service-2go-platform/edgelock-2go:EDGELOCK-2GO

## EdgeLock?? SE050
It is a plug and secure element that offers enhanced common criteria EAL 6+ based security, for unprecedencted protection against the latest attack scenerios. This ready to use secure element for IoT devices delivers end to end security (edge to cloud) without the need of security code. 

https://www.nxp.com/products/security-and-authentication/authentication/edgelock-se050-plug-trust-secure-element-family-enhanced-iot-security-with-maximum-flexibility:SE050





[Git based remote firmware update of a crossover MCU]: https://github.com/SCRATCh-ITEA3/imxrt1060-fwupdate-via-git
[LPC8N04 Application notes]:https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/general-purpose-mcus/lpc800-cortex-m0-plus-/low-cost-microcontrollers-mcus-based-on-arm-cortex-m0-plus-core:LPC8N04?&tab=Documentation_Tab&linkline=Application-Note
[Android Smartphone application]:https://www.nxp.com/design/designs/lpc8n04-development-board-for-lpc8n04-mcu:OM40002#t755
[Docker]:https://www.docker.com/
[GitHub Actions]:https://github.com/features/actions
[NXP MCUXpresso IDE]:https://mcuxpresso.nxp.com/en/welcome
[lwIP]:https://savannah.nongnu.org/projects/lwip/
[Mbed TLS]:https://tls.mbed.org/