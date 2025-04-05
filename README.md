# X509-Certificate-Template-Prototype

## Table of content
1. [Project Overview](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main#project-overview)
2. [Fundamentals](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main#fundamentals)
3. [Organization and current state](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#organization-and-current-state)
   - [Let’s See What OpenWISP Can Do Currently](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#lets-see-what-openwisp-can-do-currently-step-by-step)
         1. [Template section](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#template-section)
         2. [VPN server section](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#vpn-server-section)
         3. [Access Credential section](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#access-credentials-section)
         4. [Device group section](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#device-groups-section)
         5. [Certificate Authority section](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#certificate-authority-ca-section)
         6. [Certificate section](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#certificates-section)
4. [Approach to Project](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#approach-to-project)
    -[Let’s See What my approach will be through project, Step by Step](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#lets-see-what-my-approach-will-be-through-project-step-by-step)
        1. [what Programming laguagues we are using and why?](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#what-programming-laguagues-we-are-using-and-why)
        2. [Lets walk through file selection and pseudocode](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#lets-walk-through-file-selection-and-pseudocode)
5. [Let’s See How OpenWISP will look like after this feature](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#lets-see-how-openwisp-will-look-like-after-this-feature-step-by-step)
6. [Reference](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/tree/main?tab=readme-ov-file#references-which-i-have-followed)

## Project Overview
The X.509 Certificate Generator Templates aims to enhance the platform by adding a new feature that allows users to create X.509 certificates for secure browsing and other purposes, such as securing websites, or software signing, etc whereas it currently on supporting OpenVPN tunnels. 
Right now, OpenWISP uses a Certificate Authority (CA) to generate certificates exclusively for OpenVPN, which creates secure tunnels for data but it requires more support use cases like website security as users requests. 
With this project, I’ll create a template which enables users to generate their own certificates by selecting a CA to sign the certificate, which ensuring trusted and secure access. 
The followings things that a user can processed with:
- They can set options like the certificate duration (e.g., 1 year) to define how long the certificate remains valid.
- There is the key length (e.g., 2048-bit) to determine the strength of the security key—a long string of characters that keeps the certificate secure.
- There is the digest algorithm (e.g., SHA-256), which acts like a digital security stamp to verify the certificate’s authenticity.
  
Once these are created the certificates includs a public key, private key, and a unique ID can be applied to a user’s system, such as a web server for HTTPS or a device for secure communication. 
1. My tasks include building this template system using Python, Django, JavaScript, and openwisp-controller integrating it with OpenWISP’s configuration to make certificate details available for devices. Writing automated test cases to ensure everything works correctly.
2. Creating a detailed documentation guide with step-by-step instructions.
3. Producing a short video demonstration to show how the feature works.


## Fundamentals

**What is X509 Certificate**:
It is like a Digital ID card, in terms of networks they are like proves for a device, or website who they say they are. ex: When we visit the website which is not secured we 
get a warning message saying that *Your connection to this site is not secure*.

**What it does**: It gives permissions to allow into devices and websites. <ins>*This device is who it claims to be*</ins>.

**What is a template**: They are like the blueprints. They are used whenever they is a need of certificate to be created, its like frontend.

**How they look like**: The template includes key fields and information that describes whole x509 certificate.

![Template](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/image1.jpg)

**What is Certificate Authority**: Its like a main head of the internet provider, just like a trusted group which signs the certificates.

**What is the role of Certifivate Authority**: As they are the trusted group which signs certificates to say *Yes, this website or device is real*.

**Architecture of X509 certificate**: 

![Class diagram of x509 certificate](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/image2.jpg)

**What are the terms**:

1. **Duration**: Certificates aren’t forever—they expire. We will let users decide how long their certificate works it can be in days such as 365days,or it may be in period of 
months 3months or 6months etc. This keeps things safe—if someone steals it, it won’t last long.

3. **Key Length**: Its like a lock for a treasure. In our case it is superstrong of 2048-bit key.

4. **Digest Algorithm**: This is like a special signature on the certificate.

**Why we need X509 Certificate**:
We need secure communication and verifying digital identities, acting as a digital passport for websites, individuals, and organizations, ensuring secure transactions and  
building trust in online interactions.

**What it can do more**:
It can do digital signatures(project aim), client authentication, and securing email(current status) and device communications.


## Organization and current state

**What is OpenWISP**:It’s an open-source tool that helps users manage lots of network devices from one place. We can set them up, check if they’re working, and fix problems, 
all without running around to each device. Like a mediator.

**Why OpenWISP needs X509 ceritificates**: To secure network communications, like VPN tunnels, by verifying device identities and encrypting data.

**What is the usecase of this**: for OpenVPN to create secure connections between devices, ensuring safe management of networks.

**Current Situation**
OpenWISP can make X.509 certificates by helping devices connect to OpenVPN. OpenVPN is a tool that builds those secret tunnels, so data stays private over the 
internet. When we set up a VPN in here, it automatically creates certificates for the devices using that VPN.

### Let’s See What OpenWISP Can Do Currently, Step by Step
When we visit the website [https://demo.openwisp.io/admin/](https://demo.openwisp.io/admin/) we see a homepage interface with a sidebar menu on the left, main content in the middle-right, and a header on top.

![Home Page](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/homepage.jpg)

My major task relates to two content menu items, which deal with X509 certificates and templates:

![Configration menu](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/configuration%20menu.jpg)

![CAs and Certificate menu](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/certificate%20menu.jpg)

#### Template section

In the configuration menu, there is a "Template" field. Clicking it reveals an interface like the one below. Here, the template handles configurations such as VPN settings, with details provided for:
- **Name**: VPN Client Template
- **Type**: The type of template (determines which features are available).
- **Organization**: Which group the template belongs to.
- **Enabled by Default**: Whether new configurations will have this template enabled by default.

[Template Home](https://demo.openwisp.io/admin/config/template/)

![Template home ](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/templatefirst.jpg)

[Add Template](https://demo.openwisp.io/admin/config/template/add/)

![Add Template ](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/templatesecond.jpg)

#### VPN Server Section
The next section is the VPN server, which shows how certificates are tied to VPNs.

[VPN Server](https://demo.openwisp.io/admin/config/vpn/)

![VPN server ](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/vpnserver.jpg)

#### Access Credentials Section
The access credentials section shows how an organization manages secure connections to devices, with fields like:
- **Name**: The credential’s name (e.g., “SSH Key for Devices”).
- **Type**: The type of credential (e.g., “SSH”).

[Access Credentials](https://demo.openwisp.io/admin/connection/credentials/)/

![Access credentials](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/credentials.jpg)

#### Device Groups Section
In the device groups section, we see a list of device groups. Device groups can have VPN templates assigned to them, potentially using templates to organize devices.

[Device Group](https://demo.openwisp.io/admin/config/devicegroup/)

![device group](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/devicegroup.jpg)

#### Certificate Authority (CA) Section
In the CA section, we see a list of Certificate Authorities with columns like:
- **Name**: The CA’s name (e.g., “My CA”).
- **Created**: When the CA was created.
- **Valid Until**: When the CA expires.
- **Details**: Clicking “Add CA” or editing a CA shows a form with fields like:
  - **Operation Type**: “Create new” (to make a new CA) or “Import Existing” (to upload an existing CA).
  - **Name**: A name for the CA.
  - **Certificate and Private Key**: Fields to upload these if importing.
If creating a new CA, users can set its duration, key length, etc. This is where users manage CAs, which are used to sign certificates. Currently, these CAs are mainly used for OpenVPN certificates, as seen in the VPN server section.

[CA](https://demo.openwisp.io/admin/pki/ca/)

![CA](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/CA.jpg)

#### Certificates Section
In the certificates section, we see a list of X509 certificates with columns like:
- **Name**: The certificate’s name (e.g., “VPN Server Cert”).
- **CA**: The Certificate Authority that signed it.
- **Serial Number**: A unique ID for the certificate.
- **Valid Until**: When the certificate expires.
- **Details**: Clicking “Add Certificate” or editing a certificate shows a form with fields like:
  - **Operation Type**: “Create new” or “Import Existing.”
  - **CA**: A dropdown to pick the CA that will sign this certificate.
  - **Name**: A name for the certificate.
  - **Certificate and Private Key**: Fields to upload these if importing.
Certificates here are mostly created for OpenVPN (e.g., for VPN servers or clients).

[Certificates](https://demo.openwisp.io/admin/pki/cert/)

![certificate 1](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/certificatefirst.jpg)

![certificate 2](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/certificatesecond.jpg)


#### Certificates and OpenVPN
Right now, OpenWISP’s certificate system (under “PKI” > “Certificates”) is tied to OpenVPN. When you set up an OpenVPN server (in “Config” > “VPN”), OpenWISP uses a CA (from “PKI” > “CAs”) to automatically generate certificates for VPN clients. This is done through VPN templates (in “Config” > “Templates”).

There’s no option to create a certificate template for general purposes (e.g., for a website or IoT device). Certificates are only generated as part of the VPN setup process.

## Approach to project
### Let’s See What my approach will be through project, Step by Step
There are the **major** tasks:
**Implement a new certificate template type in OpenWISP to support general-purpose x509 certificate generation.**
**Allow users to select a CA and configure certificate properties.**
**Integrate with OpenWISP's configuration management to expose certificate details (public key, private key, and UUID) as variables for automated deployment.**

Lets make this task more general:
1. Add a new “Certificate” template type with fields for CA and certificate properties.
2. Update the website interface to show these fields and allow CA selection.
3. Modify the certificate generation process to use the template.
4. Integrate the certificate details into OpenWISP configuration system as variables (public key, private key, and UUID).

#### **what Programming laguagues we are using and why?**
We are going to use these Python, Django, and JavaScript. And the integrating this languages going to be done on Openwisp-controller repository which handles CA, django_x509(PKI) and others.

<ins> Python </ins> is the primary programming language used for the server-side application (web admin, API, controller, workers). In this project it defines the new Template type and fields for models.py and handles the logic for generating certificates and exposing variables.

<ins> Django </ins> the most popular web frameworks for Python. It is used extensively in our modules, allowing rapid development and access to a rich ecosystem. Django’s admin.py module creates the UI for the new template type, and its forms.py system ensures users can select a CA and configure properties.

<ins> JavaScript </ins> A language for adding interactivity to web pages. This are used to for making admin, forms dynamic while showing certificate-specific fields only when the “Certificate” type is selected.

**overall** *Python + Django*: Handle the backend logic (models, certificate generation, configuration integration) and generate the admin UI. *JavaScript*: Adds frontend interactivity, making the form user-friendly.

#### Lets walk through file selection and pseudocode
**<ins> models.py </ins>** [openwisp-controller config models file](https://github.com/openwisp/openwisp-controller/blob/master/openwisp_controller/config/models.py): 

From this file we get to know that there is are template models, configuration-relation which are created that stands out to be the data structure for creating our new Certificate model in it. I need to add a new “Certificate” template type and fields (like CA, duration, key length, digest algorithm) to support general-purpose X.509 certificate generation.

**pseudocode**
```
#new “Certificate” template type and fields for CA and properties.

class Template:
  duration=INTEGER/DATE
  private_key=STRING/GENERIC
  ca = Certificate Authority refering other table
  digest_algorithm=CHOICEFIELD("SHA-256","SHA-512")

  def generate_certificate(self):
    duration=self.duration,
    private_key=self.private_key,
    ca=self.ca,
    digest_algorithm=self.digest_algorithm
```

**<ins> admin.py </ins>** [openwisp-controller config admin file](https://github.com/openwisp/openwisp-controller/blob/master/openwisp_controller/config/admin.py): 

It customizes the django admin interface for the config module’s models like Templates. I need to update the admin UI to show a form for the new “Certificate” template type, allowing users to select a CA and configure properties (duration, key length, digest algorithm).

**pseudocode**
```
#admin customizes the UI to show the form.

class TemplateAdmin:
    #additional fields to display like name, type, organization same as OpenVPN tunnals
    list_display = [
        "name",
        "type",
        "ca",
        "organization",
    ]
    form = TemplateForm

    class Media:
        #create js file to make interface dynamic
        js = template_form.js
```

**<ins> forms.py </ins>** 

Forms in Django handle user input, validation, and rendering in the admin interface. I need a form to collect and validate the new certificate-specific fields (CA, duration, etc.) when users create or edit a certificate template.

**pseudocode**
```
#formshandles form logic and validation

class TemplateForm:
    fields = [
      "name",
      "type",
      "organization",
      "ca"
      "duration",
      "key_length",
      "digest_algorithm"
    ]

    def validate():
        #additional constraints
        if type=certificate:
            if no ca :
                message "CA is required"
        #default make them
        else:
            self.ca = None
            self.duration = None
            self.key_length = None
            self.digest_algorithm = None
```

**<ins> admin.py </ins>** [openwisp-controller pki admin file](https://github.com/openwisp/openwisp-controller/blob/master/openwisp_controller/pki/admin.py): 

This file customizes the admin interface for the pki module, which handles Certificate Authorities (CAs) and certificates using the django-x509 library. I need to allow users to generate certificates using my new template, which involves adding a “Generate from Template” option in the certificate creation form.

**pseudocode**
```
Modifies the certificate admin UI to support template-based generation.

class CertificateAdmin:
    list_display = [
        "name",
        "ca",
        "valid"
    ]
    form = CertificateForm

class CertificateForm:
    operation_type = ChoiceField(choices=[
        //has it is in certificate pki(https://demo.openwisp.io/admin/pki/cert/add/)
        "create_new", 
        "import_existing",
        "generate_from_template",
    ])
    template = Template.objects.filter(type="certificate")//check their existence

    def save():
        if operation_type==true
            self.name = name
            self.ca = ca
            self.public_key = public_key
            self.private_key =private_key
            self.uuid = generate_uuid()
            self.valid = cert.valid
        save_to_database()
```

## Let’s See How OpenWISP will look like after this feature, Step by Step

Let’s walk through how the UI will change, focusing on the website dashboard and the new feature.


#### 1. Templates Section ([https://demo.openwisp.io/admin/config/template/](https://demo.openwisp.io/admin/config/template/))
   
**What’s New:** There will be a new template type called “Certificate Template.”

**What It Looks Like:** In the “Templates” section, the list of templates now includes a new template type. Based on `TemplateAdmin` in `admin.py`, it displays:

- **Name**: e.g., "Website Certificate Template"
- **Type**: "Certificate" (new type from `models.py`)
- **CA**: The Certificate Authority linked to this template (from `ca` in `models.py`)
- **Organization**: The group this template belongs to

**Add Template Form:** When you click “Add Template,” the form now has a new option in the “Type” dropdown: “Certificate.” Selecting this type changes the form (via `template_form.js` from `admin.py`) to show certificate-specific fields from `TemplateForm` in `forms.py`:

- **Name**: e.g., "Website Certificate Template"
- **CA**: Dropdown to select a Certificate Authority (required per `validate()` in `forms.py`)
- **Duration**: Integer or date field (e.g., "365" days, from `models.py`)
- **Key Length**: Integer field (e.g., "2048", from `forms.py`)
- **Digest Algorithm**: Dropdown with "SHA-256" or "SHA-512" (from `models.py`)
- **Save Button**: Submits the form

**How It Works:** After saving, this template can be used to generate certificates for any purpose like securing a website. Users can assign this template to devices or use it manually to create certificates, leveraging the `generate_certificate` method in `models.py`.


#### 2. Certificates Section ([https://demo.openwisp.io/admin/pki/cert/](https://demo.openwisp.io/admin/pki/cert/))

**What’s New:** Users can now generate certificates using your new template.

**What It Looks Like:** In the “Certificates” section, there’s a new way to create certificates. When you click “Add Certificate,” the form (from `CertificateForm` in `pki/admin.py`) now has an option to use a template:

- **Options**: Dropdown with "create new", "import", "Generate from Template" (new option from `operation_type` in pseudocode)
- **Template**: If we pick “Generate from Template,” a new dropdown appears to select your certificate template (filtered via `Template.objects.filter(type="certificate")`).
- **Name**: A text box to name the certificate (e.g., “My Website Cert”).
- **CA, Duration, Digest Algorithm**: These fields are auto-filled from the selected template (based on `models.py`) and are required when generating from a template, per the pseudocode logic.

**Generated Certificate:** After saving, the certificate is created using the template’s settings via the `save()` method in `CertificateForm`. The list of certificates (from `CertificateAdmin.list_display`) now includes your new certificate, with details like:

- "Name": e.g., "My Website Cert"
- "CA": The CA from the template
- "Valid": Expiration date based on `duration`


#### 3. Device Groups Section ([https://demo.openwisp.io/admin/config/devicegroup/](https://demo.openwisp.io/admin/config/devicegroup/))

**What’s New:** Your certificate template can be assigned to device groups.

**What It Looks Like:** In the “Device Groups” section, the “Templates” field includes a new certificate template (e.g., "Website Certificate Template") in the list of available templates, consistent with the `Template` model’s integration.

#### 4. CA Section ([https://demo.openwisp.io/admin/pki/ca/](https://demo.openwisp.io/admin/pki/ca/))

**What’s New:** No changes to the CA section itself, but new template uses these CAs.

**What It Looks Like:** The CA section remains as is, but the `ca` field in the `Template` model links to these CAs, ensuring they are used when generating certificates via the new template.



## References which i have followed

1. <sup>Medium</sup>      (Takahiko Kawasaki)    <ins>Illustrated X.509 Certificate</ins>

    I gained a visual understanding of X.509 certificate structure and templates, as defined in RFC 5280, through detailed diagrams and explanations.

    https://darutk.medium.com/illustrated-x-509-certificate-84aece2c5c2e 
    ![Certificate Structure](https://github.com/SitaGanesh/X509-Certificate-Template-Prototype/blob/main/Images/certificateStructure.jpg)


2. <sup>Medium </sup> (seantywork)    <ins>Fundamentals of Secure Communication X509 Certificate</ins>

    I learned the basics of secure communication using OpenSSL, which provided practical visualization and a strong foundation for understanding X.509 certificates.

    https://medium.com/@seantywork/fundamentals-of-secure-communication-x509-certificate-6bcfd522a5d1


3. <sup>YouTube</sup>  (OneMircFifty)     <ins>X.509 Certificate Video (Part 1, with Parts 2 and 3 referenced)</ins>

    I understood X.509 certificates from scratch through a comprehensive video series that broke down concepts step-by-step across multiple parts. 

    https://youtu.be/kAaIYRJoJkc?si=J6U3NlSgPgESEEHn


4. <sup>YouTube</sup>   (Secure Soft)     <ins>X.509 Certificate Generator</ins>

    What I Learned: I discovered a multipurpose certificate utility tool by Secure Soft via a short 2-minute video, showcasing how to generate X.509 certificates.

    https://youtu.be/RMy-KPq20Hw?si=HCYmNiZY9Lj9-Rwg


5. <sup>Hexdocs</sup>    (X509.Certificate.Template)       <ins>Documentation</ins>

    I explored technical documentation detailing X.509 certificate templates, enhancing my understanding of their programmatic structure and usage.

    https://hexdocs.pm/x509/X509.Certificate.Template.html 
