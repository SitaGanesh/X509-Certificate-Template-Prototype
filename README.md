# X509-Certificate-Template-Prototype

## Project Overview
The X.509 Certificate Generator Templates aims to enhance the platform by adding a new feature that allows users to create X.509 certificates for secure browsing and other purposes, such as securing websites, or software signing, etc whereas it currently on supporting OpenVPN tunnels. 
Right now, OpenWISP uses a Certificate Authority (CA) to generate certificates exclusively for OpenVPN, which creates secure tunnels for data but it requires more support use cases like website security as users requests. 
With this project, I’ll create a template which enables users to generate their own certificates by selecting a CA to sign the certificate, which ensuring trusted and secure access. 
The followings things that a user can processed with:
- They can set options like the certificate duration (e.g., 1 year) to define how long the certificate remains valid.
- There is the key length (e.g., 2048-bit) to determine the strength of the security key—a long string of characters that keeps the certificate secure.
- There is the digest algorithm (e.g., SHA-256), which acts like a digital security stamp to verify the certificate’s authenticity.
  
Once these are created the certificates includs a public key, private key, and a unique ID can be applied to a user’s system, such as a web server for HTTPS or a device for secure communication. 
- My tasks include building this template system using Python, Django, JavaScript, and openwisp-controller integrating it with OpenWISP’s configuration to make certificate details available for devices. Writing automated test cases to ensure everything works correctly.
- Creating a detailed documentation guide with step-by-step instructions.
- Producing a short video demonstration to show how the feature works.


## Fundamentals

**What is X509 Certificate**:
It is like a Digital ID card, in terms of networks they are like proves for a device, or website who they say they are. ex: When we visit the website which is not secured we get a warning message saying that *Your connection to this site is not secure*.

**What it does**: It gives permissions to allow into devices and websites. *This devie is is who it claims to be*.

**What is a template**: They are like the blueprints. They are used whenever they is a need of certificate to be created, its like frontend.

**How they look like**: The template includes key fields and information that describes whole x509 certificate.
![Template image](C:\Users\User\OneDrive\Pictures\Other\image1.jpg)

**What is Certificate Authority**: Its like a main head of the internet provider, just like a trusted group which signs the certificates.

**What is the role of Certifivate Authority**: As they are the trusted group which signs certificates to say *Yes, this website or device is real*.

**Architecture of X509 certificate**: 
![Class diagram of x509 certificate](C:\Users\User\OneDrive\Pictures\Other\image2.jpg)

**What are the terms**:

1. **Duration**: Certificates aren’t forever—they expire. We will let users decide how long their certificate works it can be in days such as 365days,or it may be in period of months 3months or 6months etc. This keeps things safe—if someone steals it, it won’t last long.

2. **Key Length**: Its like a lock for a treasure. In our case it is superstrong of 2048-bit key.

3. **Digest Algorithm**: This is like a special signature on the certificate.

**Why we need X509 Certificate**:
We need secure communication and verifying digital identities, acting as a digital passport for websites, individuals, and organizations, ensuring secure transactions and building trust in online interactions. 

**What it can do more**:
It can do digital signatures(project aim), client authentication, and securing email(current status) and device communications.


## Organization and current state
