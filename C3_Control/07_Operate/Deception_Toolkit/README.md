# <img src="../../../images/operate.png" alt ='operate'  width="10%" > SCRATCh - DevOps - Operate Tools - Deception Toolkit


[![SCRATCh - funded by BMBF](https://img.shields.io/badge/part%20of-SCRATCh-yellow)](https://scratch-itea3.eu/)
![SCRATCh - funded by BMBF](https://img.shields.io/badge/funded%20by-BMBF-blue)
[![ITEA3](https://img.shields.io/badge/supported%20by-ITEA3-orange)](https://www.itea3.org)

Deception Toolkits: The purpose of this tool is to impede the reconnaissance phase of an attacker. According to the Lockheed Martin Cyber Kill Chain, this phase is the first in a series of hostile activities. A directed manipulation of the hostile reconnaissance output therefore affects the entire process of hostile activity. Ideally, deception allows immediate impact on the prevention of an attack.

## Overview
In classical security operations an asymmetry between attackers and defenders exist, where defenders cannot afford to make any mistake, whereas the attacker has unlimited time and attempts to find a mistake. Deception may help to give the defender the advantage of detecting malicious attempts, while causing uncertainty and precaution for the attacker. Bell and Whaley distinguish two modes of deception
- simulation or showing the false by  mimicking, inventing or decoying
- dissimulation or hiding the truth by masking, repackaging or dazzling

In SCRATCh we propose a toolkit, which allows to augment existing HTTP(S) and SSH Services with deception strategies. To facillitate the adoption, these decoys are placed through a reverse proxy. Therefore no modification of the services is needed. 

## HTTP Deception Proxy

The HTTP Deception Proxy allows to catch and modify HTTP responses of the HTTP server. In case the requested page does not exist, the proxy can provide an invented decoy document. Such decoys could be injecting HTML comments which lead to a [honey file](https://ieeexplore.ieee.org/document/1437806) or contain [honey credential](https://people.csail.mit.edu/rivest/honeywords/), injecting entries into the [Robots Exlusion File](https://en.wikipedia.org/wiki/Robots_exclusion_standard) or [Sitemap](https://en.wikipedia.org/wiki/Site_map). Any interaction with the pointed to honeyfile or honey credentials will raise an alert.

The HTTP Deception Proxy developed within the SCRATCh Project was proposed in this Publication for the Moving Target Defense Workshop on the ACM CCS conference: 
Daniel Fraunholz, Daniel Reti, Simon Duque Anton, and Hans Dieter Schotten. 2018. Cloxy: A Context-aware Deception-as-a-Service Reverse Proxy for Web Services. In Proceedings of the 5th ACM Workshop on Moving Target Defense (MTD '18). Association for Computing Machinery, New York, NY, USA, 40–47. DOI:https://doi.org/10.1145/3268966.3268973 [[PDF](https://dl.acm.org/doi/pdf/10.1145/3268966.3268973?casa_token=jlVZ7fpJoMMAAAAA:XinoziNFSc-kv5vt3ykzPEaMhjwR4hJklkJJbli8BJXPZsoJ3WjOpv6M_ESgKdKKww4H6pX8VBV-)] 

See the Gitlab repository for further information:

https://dfki-3055.dfki.de/esca/esca-http-proxy/

## SSH Deception Proxy

The SSH Deception Proxy is a framework for placing decoy elements through an SSH proxy, allowing to deploy decoy elements on-the-fly without the need for a modification of the protected host system.

### Deception Tokens
Fake files should seem to be part of the host’s file system.
This lends itself readily for several features:
- Honey Files: Honey files can be added to command output. For example fake credentials in /passwords.txt can be added. When using these credentials to connect to the host, the proxy catches their usage and can stop the IP from reconnecting, redirect the connection into a sandbox, or implement other appropriate countermeasures.
- Overwriting critical information contained in files: Some files, such as /proc/version, contain critical information which can reveal weaknesses about the host. These files can be either overwritten with wrong information, making the attacker waste time on exploiting vulnerabilities fixed in previous versions or their content can be hidden completely. Since ”everything is a file” in Linux, most configuration information can be faked.

See the GitHub repository for further information:

https://github.com/SCRATCh-ITEA3/esca-ssh-proxy


The SSH Deception Proxy developed within the SCRATCh Project was described in this publication: 
D. Reti, D. Klaaßen, S. D. Anton and H. Dieter Schotten, "Secure (S)Hell: Introducing an SSH Deception Proxy Framework," 2021 International Conference on Cyber Situational Awareness, Data Analytics and Assessment (CyberSA), 2021, pp. 1-6, doi: https://doi.org/10.1109/CyberSA52016.2021.9478201 [[PDF](https://arxiv.org/pdf/2104.03666)

## Dashboard

A dashboard is in devolopedment to present the collected alerts and configure the decoy elements.

