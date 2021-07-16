# <img src="../../images/code.png" alt ='code'  width="10%" > SCRATCh - DevOps - Code Tools - OWASP Dependency Track

# Introduction to OWASP Dependency Track and OWASP Dependency Track Github Action  
[OWASP Dependency Track] checks vulnerability, license, and quality risks in a real-time software bill of materials. Dependency-Track is an intelligent Supply Chain Component Analysis platform that allows organizations to identify and reduce risk from the use of third-party and open source components. Dependency-Track takes a unique and highly beneficial approach by leveraging the capabilities of Software Bill of Materials (SBOM). This approach provides capabilities that traditional Software Composition Analysis (SCA) solutions cannot achieve.

The Software Bill of Materials (SBOM) is a list of components in a piece of software. It fully describes the components in a product so it is important to find out if any of the components, typically external libraries have any known vulnerability which can compromise the security of the software. 
OWASP Dependency Track analyze the SBOM and generates an exhaustive report including all the vulnerabilities found along with the licenses of all the components. 

The full process is depicted in the image below.

![image](https://user-images.githubusercontent.com/4015457/124102330-8d767b80-da60-11eb-8234-9c9b04458e3a.png)

In order to be able to include the vulnerability check in the CI/CD cycle, **Quobis developed a Github action which generates the SBOM from any existing project and update it to any OWASP Dependency Track instance whose REST API is accessible through Internet**. The Github action can be used directly from the Github repository, without requiring any additional service. When the action is triggered by developer actions, for example a merge in the master branch, then Github instantiates a container with the software needed to generate the SBOM and upload it to the server.  
Many other actions can be smoothly added to the  or even connected to this action. The project must follow the standard structure and only Python, Golang and Nodejs projects are supported so far.

# How to use OWASP Dependency Track

* In order to get access to a public instance of OWASP Dependency Track please, access the repository below. You will need to ask for an account:
[[OWASP Dependency Track action repository]](https://github.com/Quobis/action-owasp-dependecy-track-check)

* Once you get the acount, and in order to test to use the action in any existing repository you can import the action directly from the Github Marketplace: 
[[owasp-dependency-track-check action in the Github marketplace]](https://github.com/marketplace/actions/owasp-dependency-track-check)

