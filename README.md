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



<!-- NIST LOGO -->
<br />
<div align="center">
  <a href="https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-53r5.pdf">
    <img src="https://i.imgur.com/XRn0OuK.png" alt="NIST Logo" width="250" height="250">
  </a>

  <p align="center">
    This write up demonstrates how to apply NIST SP 800-53 SC-7 Boundary Protection to resources within Microsoft Azure.
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
NIST SP 800-53, provides a catalog of guidelines to help federal agencies and organizations implement security and privacy controls. It includes controls across areas like access control, incident response, and risk assessment, supporting compliance with the Federal Information Security Modernization Act (FISMA). Control SC-7, Boundary Protection, requires organizations to monitor and control communications at system boundaries to prevent unauthorized access. It involves using firewalls, proxies, and gateways to secure network communications and protect sensitive data.

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- ENVIRONMENT -->
## Environment

The environment used in this write-up was deployed in Microsoft Azure with key vaults, network security groups, storage accounts, and virtual machines (Windows and Linux). These resources were then configured to be accessible accessible to the public internet, placing them at a high risk of unauthorized access.

### Prerequisites

1. Microsoft Azure Account
2. Azure Key Vault (AKV)
3. Azure Storage Account
4. Linux Virtual Machine (VM)
5. Windows Virtual Machine VM)
6. Network Security Groups (NSG)
7. Microsoft Defender for Cloud

### Configuration

1. Add an Inboud Rule to the Linux and Windows VM NSG, which allows any type of traffic to any port.
<img src="https://i.imgur.com/ouSsDqk.png" alt="NSG Any Inbound Rule" width="500" height="750">
2. Turn off Windows Firewall on the Windows VM.
<img src="https://i.imgur.com/czWdLZ2.png" alt="Turn off Windows Firewall" width="500" height="500">

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- IMPLEMENTATION -->
## Implementation

To implement NIST SP 800-53 compliance in Azure, Microsoft Defender for Cloud should already be enabled.


<img src="https://i.imgur.com/rzvZpV5.png" alt="NIST SP 800-53 Off" width="750" height="250">
<img src="https://i.imgur.com/rbXESji.png" alt="NIST SP 800-53 On" width="750" height="250">

Once activated, Microsoft Defender for Cloud allows NIST SP 800-53 compliance to be applied to Azure resources and subscriptions, providing a dashboard with detailed compliance data and tailored recommendations. This dashboard offers a centralized view of compliance status, with actionable insights to help align resources with NIST standards.

<img src="https://i.imgur.com/Syi4iTu.png" alt="NIST SP 800-53 Dasboard" width="750" height="750">

With NIST SP 800-53 compliance activated in Azure, controls such as the SC-7 Boundary Protection can be viewed in detail. As shown below, the current environment is not complaint with the recommended controls.

<img src="https://i.imgur.com/AafuPQZ.png" alt="SC-7 Boundary Protection Recommendations" width="1000" height="200">

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- REMEDIATION-->
## Remediation
The following actions are required to achieve NIST SP 800-53 SC-7 Boundary Protection compliance with the current Azure resources and environment.

*Subnets should be associated with a network security group:*
- [x] Create private endpoint for the Azure Key Vault.
<img src="https://i.imgur.com/3nsR0x2.png" alt="AKV Private Endpoint" width="500" height="500">

- [x] Create private endpoint for the Azure Storage Account.
<img src="https://i.imgur.com/jjC13Xm.png" alt="SA Private Endpoint" width="500" height="500">

*Management ports should be closed on your virtual machines:*
- [x] Turn on the Windows Firewall on the Windows VM.
- [x] Remove the Inbound Rule from the Linux & Windows VM NSG which allows inbound traffic on any port.

*Management ports of virtual machines should be protected with just-in-time network access control:*
- [x] Enable Just-in-time VM access via Microsoft Defender for Cloud Workload protections.

*All network ports should be restricted on network security groups associated to your virtual machine:*
- [x] Add Inbound Rule to Linux & Windows VM NSG which allows traffic from admin IP address only.
<img src="https://i.imgur.com/qtP5a6u.png" alt="NSG Admin Only Inbound Rule" width="500" height="500">

*Azure Kev Vaults should use private link:*
- [x] Disable Azure Key Vault public access.
<img src="https://i.imgur.com/TDUTUUR.png" alt="Disable Azure Key Vault Public Access" width="500" height="500">

<p align="right">(<a href="#readme-top">back to top</a>)</p>



<!-- CONCLUSION -->
## Conclusion
In summary, the adjustments to the Azure resources greatly strengthened the security posture of the environment by aligning with NIST SP 800-53 SC-7 Boundary Protection controls. Measures like restricting inbound and management ports, along with implementing private endpoints, effectively mitigated high network exposure risks. Together, these adjustments provide a stronger defense against unauthorized access, reduce potential attack vectors, and reinforce boundary protection within the Azure environment, underscoring the effectiveness of NIST SP 800-53 in safeguarding organizations against cyber threats.

<p align="right">(<a href="#readme-top">back to top</a>)</p>
