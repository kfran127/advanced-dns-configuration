<p align="center">
  <img src="https://github.com/user-attachments/assets/a9e62984-6877-41d3-b24c-25d0460b9005" alt="Microsoft Azure Banner">
</p>

<h1>Advanced DNS Configuration in Active Directory within Azure VMs</h1>

<p>In this lab, I focused on configuring advanced DNS settings within an Active Directory environment using Azure Virtual Machines. By the end of this lab, I successfully managed DNS records, handled local DNS cache, and configured both A-records and CNAME records to enhance network management within a domain environment.</p>

<h2>Part 1: A-Record Configuration</h2>

<p><strong>Step 1: Connect to the Virtual Machines</strong></p>
<ul>
  <li>I turned on both <strong>DC-1</strong> and <strong>Client-1</strong> in the Azure Portal to ensure they were online.</li>
  <li>I connected to <strong>DC-1</strong> using my domain admin account: <strong>mydomain.com\pablo_davis</strong>.</li>
  <li>Then, I connected to <strong>Client-1</strong> using the same domain admin account: <strong>mydomain\pablo_davis</strong>.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3982d64a-c707-4807-a394-af99f62ca93a" alt="A-Record Configuration Image" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/14b798ff-f668-4630-914e-f7e619ca0282" alt="A-Record Configuration Image" width="80%">
</p>


<p><strong>Step 2: Testing DNS</strong></p>
<ul>
  <li>From <strong>Client-1</strong>, I attempted to ping the hostname <strong>"mainframe"</strong> but observed that it failed since there was no DNS record yet for “mainframe.”</li>
  <li>I then ran <strong>nslookup mainframe</strong> on <strong>Client-1</strong>, which confirmed the absence of a DNS record for the hostname.</li>
</ul>
<p align="center">
  <img src="https://github.com/user-attachments/assets/3696fcc1-de96-4c1e-830e-31037cc888b0" alt="Testing DNS Image" width="80%">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/d4857fa6-a0dc-4073-9462-e2ac28022d80" alt="Testing DNS Image" width="80%">
</p>



<p><strong>Step 3: Create a DNS A-Record</strong></p>
<ul>
  <li>On <strong>DC-1</strong>, I opened the DNS Manager and created a new A-record for <strong>"mainframe"</strong>.</li>
  <li>I pointed this A-record to <strong>DC-1’s private IP address</strong>.</li>
  <li>Back on <strong>Client-1</strong>, I attempted to ping <strong>"mainframe"</strong> again and observed that the ping now succeeded because of the newly created A-record.</li>
</ul>

<p align="center">
  <img src="https://github.com/user-attachments/assets/e081ebad-e398-43c5-8b43-a163083cf63a" alt="Create A-Record Image" width="80%">
</p>


<p align="center">
  <img src="https://github.com/user-attachments/assets/27ecae75-a45e-404d-988d-b27c62f38c5d" alt="Create A-Record Image" width="80%">
</p>



<h2>Part 2: Local DNS Cache Management</h2>

<p><strong>Step 4: Modify the DNS Record</strong></p>
<ul>
  <li>To test DNS cache behavior, I modified the <strong>mainframe</strong> A-record on <strong>DC-1</strong> to point to <strong>8.8.8.8</strong> (Google's DNS).</li>
  <li>Back on <strong>Client-1</strong>, I pinged <strong>"mainframe"</strong> again and observed that it still pinged the old address, as the local DNS cache had not yet updated.</li>
</ul>
<p align="center">
  <img src="IMAGE_URL_HERE" alt="Modify DNS Record Image" width="80%">
</p>

<p><strong>Step 5: View and Flush the DNS Cache</strong></p>
<ul>
  <li>On <strong>Client-1</strong>, I opened PowerShell and ran <strong>ipconfig /displaydns</strong> to observe the local DNS cache.</li>
  <li>I then flushed the DNS cache using <strong>ipconfig /flushdns</strong>.</li>
  <li>After confirming that the cache was empty by running <strong>ipconfig /displaydns</strong> again, I attempted to ping <strong>"mainframe"</strong> once more and observed that the ping resolved to the new address <strong>8.8.8.8</strong>.</li>
</ul>
<p align="center">
  <img src="IMAGE_URL_HERE" alt="Local DNS Cache Image" width="80%">
</p>

<h2>Part 3: CNAME Record Configuration</h2>

<p><strong>Step 6: Create a CNAME Record</strong></p>
<ul>
  <li>Back on <strong>DC-1</strong>, I created a CNAME record that pointed the hostname <strong>"search"</strong> to <strong>www.google.com</strong>.</li>
  <li>On <strong>Client-1</strong>, I pinged <strong>"search"</strong> and observed the redirection to Google's IP address due to the CNAME record.</li>
  <li>Finally, I ran <strong>nslookup search</strong> on <strong>Client-1</strong> to confirm the results of the CNAME record configuration.</li>
</ul>
<p align="center">
  <img src="IMAGE_URL_HERE" alt="CNAME Record Configuration Image" width="80%">
</p>

<h2>Conclusion</h2>
<p>In this lab, I successfully configured advanced DNS settings in an Active Directory environment using Azure Virtual Machines. I created A-records and CNAME records, managed DNS settings, and handled local DNS cache. These skills are vital for network management and security operations in real-world IT environments.</p>

<p><strong>Note:</strong> I made sure not to delete the VMs in Azure, as they will be used in future labs. Instead, I simply <strong>stopped</strong> the VMs within the Azure Portal to save costs.</p>
