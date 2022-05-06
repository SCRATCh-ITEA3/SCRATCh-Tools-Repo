# <img src="../../../images/release.png" alt ='release'  width="10%" > SCRATCh - DevOps - Release Tools - OTAlyzer

# OTAlyzer

[![Available](https://img.shields.io/badge/status-available-green)](https://github.com/OTARIS/Otalyzer)
[![SCRATCh - funded by BMBF](https://img.shields.io/badge/part%20of-SCRATCh-yellow)](https://scratch-itea3.eu/)
![SCRATCh - funded by BMBF](https://img.shields.io/badge/funded%20by-BMBF-blue)
[![ITEA3](https://img.shields.io/badge/supported%20by-ITEA3-orange)](https://www.itea3.org)

## A tool to automate network traffic analysis

### The OTARIS traffic analyzer (OTAlyzer) is a tool to analyze large amounts of network traffic by searching for occurences of keywords, e.g. the transmission of passwords or private data. 

The OTALyzer can assist in fulfilling common IoT security requirements such as monitoring telemetry data and ensuring confidentiality of sensitive/private data.

### Structure of the tool

Nowadays developers rely heavily on using third-party-libraries, without knowing much about their inner workings. This imposes a risk on privacy and data confidentiality, since sometimes these libraries transmit sensible information or tracking data to remote hosts.

The OTARIS traffic analyzer (OTAlyzer) is a tool to analyze large amounts of network traffic by searching for occurences of keywords, e.g. the transmission of passwords or private data. In addition to plaintext, the OTAlyzer also detects various hash-formats and outputs additional metadata for each finding, such as the location of the remote host, the TLS-ciphers it supports or the severity of a finding.

You need to feed the otalyzer keywords and severity levels via configuration files. For more information, see Configuration.

The OTAlyzer supports HTTP, HTTPS, TCP and MQTT payloads and works with `.pcap[ng]`-files, generated by e.g. [wireshark](https://www.wireshark.org/) and `.mitm`-files, which are the files generated by [mitmdump](https://mitmproxy.org/).

## Implementation & Configuration
### Installation

You can either download the binaries from the github repository under [releases](https://github.com/OTARIS/OTAlyzer/releases) or build them from source yourself using dotnet:

#### Linux 
```bash
git clone https://github.com/OTARIS/OTAlyzer/releases
cd OTAlyzer.AnalyticsWorker 
dotnet publish -c Release -p:PublishSingleFile=true --self-contained true --runtime linux-x64
```

#### Windows
```powershell
git clone https://github.com/OTARIS/OTAlyzer/releases
cd OTAlyzer.AnalyticsWorker
dotnet publish -c Release -p:PublishSingleFile=true --self-contained true --runtime win-x64
```

### Usage

See the [GitHub repository](https://github.com/OTARIS/OTAlyzer) for instructions.