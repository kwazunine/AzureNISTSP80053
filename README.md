# NIST SP 800-53 [SC-7 Boundary Protection]

<!-- Improved compatibility of back to top link: See: https://github.com/othneildrew/Best-README-Template/pull/73 -->
<a id="readme-top"></a>
<!--
*** Thanks for checking out the Best-README-Template. If you have a suggestion
*** that would make this better, please fork the repo and create a pull request
*** or simply open an issue with the tag "enhancement".
*** Don't forget to give the project a star!
*** Thanks again! Now go create something AMAZING! :D
-->



<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf">
    <img src="https://i.imgur.com/ULHBnk7.jpeg" alt="Logo" width="300" height="150">
  </a>

  <p align="center">
    This write up demonstrates how to apply NIST SP 800-53 [SC-7 Boundary Protection] to resources within Microsoft Azure.
    <br />
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-nist-sp-800-53-sc-7-boundary-protection">About NIST SP 800-53 SC-7 Boundary Protection</a>
    </li>
    <li>
      <a href="#environment">Environment</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#configuration">Configuration</a></li>
      </ul>
    </li>
    <li><a href="#implementation">Implementation</a></li>
    <li><a href="#remediation">Remediation</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ol>
</details>



<!-- About NIST SP 800-53 SC-7 Boundary Protection -->
## About NIST SP 800-53 SC-7 Boundary Protection

<img src="https://i.imgur.com/exk5sXu.png" alt="Logo" width="200" height="200">

NIST SP 800-53, provides a catalog of guidelines to help federal agencies and organizations implement security and privacy controls. It includes controls across areas like access control, incident response, and risk assessment, supporting compliance with the Federal Information Security Modernization Act (FISMA). Control SC-7, Boundary Protection, requires organizations to monitor and control communications at system boundaries to prevent unauthorized access. It involves using firewalls, proxies, and gateways to secure network communications and protect sensitive data.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ENVIRONMENT -->
## Environment

The environment is deployed in Microsoft Azure with key vaults, network security groups, and virtual machines (Windows and Linux). These resources are configured to be accessible from the public internet, placing them at a high risk of unauthorized access.

### Prerequisites

1. Microsoft Azure Account
2. Azure Key Vault
3. Azure Storage Account
4. Linux Virtual Machine
5. Windows Virtual Machine
6. Network Security Groups
7. Microsoft Defender for Cloud

### Configuration

1. Add Inboud Rule to the Virtual Machine Network Security Gorups which opens enables all traffic.
<img src="https://i.imgur.com/ouSsDqk.png" alt="Logo" width="250" height="500">
2. Turn off Windows Firewall on Windows VM.
<img src="https://i.imgur.com/czWdLZ2.png" alt="Logo" width="400" height="300">

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- IMPLEMENTATION -->
## Implementation

To set up NIST SP 800-53 compliance in Azure, begin by enabling Microsoft Defender for Cloud. Once activated, Microsoft Defender for Cloud allows NIST SP 800-53 compliance to be applied to Azure resources and subscriptions, providing a dashboard with detailed compliance data and tailored recommendations. This dashboard offers a centralized view of compliance status, with actionable insights to help align resources with NIST standards.

<img src="https://i.imgur.com/rzvZpV5.png" alt="Logo" width="500" height="150">
<img src="https://i.imgur.com/rbXESji.png" alt="Logo" width="500" height="150">
<img src="https://i.imgur.com/Syi4iTu.png" alt="Logo" width="500" height="400">

With NIST SP 800-53 activated, reviewing the SC-7 Boundary Protection recommendations is next. As shown below, the current environment is not complaint with the recommended controls.

<img src="https://i.imgur.com/AafuPQZ.png" alt="Logo" width="600" height="200">

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- REMEDIATION-->
## Remediation
The following actions are required to achieve NIST SP 800-53 SC-7 Boundary Protection compliance in the current environment.

Subnets should be associated with a network security group:
- [x] Create private endpoint for the Azure Key Vault.
<img src="https://i.imgur.com/3nsR0x2.png" alt="Logo" width="300" height="500">

- [x] Create private endpoint for the Azure Storage Account.
<img src="https://i.imgur.com/jjC13Xm.png" alt="Logo" width="300" height="500">

Management ports should be closed on your virtual machines:
- [x] Turn on the Windows Firewall on the Windows VM.
- [x] Remove the Inbound Rule from the Linux & Windows VM NSG which allows inbound traffic on any port.

Management ports of virtual machines should be protected with just-in-time network access control:
- [x] Enable Just-in-time VM access via Microsoft Defender for Cloud Workload protections.

All network ports should be restricted on network security groups associated to your virtual machine:
- [x] Add Inbound Rule to Linux & Windows VM NSG which allows traffic from admin IP address only.
<img src="https://i.imgur.com/qtP5a6u.png" alt="Logo" width="300" height="500">

Azure Kev Vaults should use private link:
- [x] Disable Azure Key Vault public access.
<img src="https://i.imgur.com/TDUTUUR.png" alt="Logo" width="500" height="500">

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONCLUSION -->
## Conclusion

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request
