<p align="center">
  <img src="https://github.com/user-attachments/assets/a9e62984-6877-41d3-b24c-25d0460b9005" alt="Microsoft Azure Banner">
</p>

<h1>Advanced DNS Configuration in Active Directory within Azure VMs</h1>

<p>This lab extends from the previous Active Directory setup and focuses on advanced DNS configurations within Azure Virtual Machines. You will learn how to manage DNS records, handle local DNS cache, and configure A-records and CNAME records within an Active Directory environment.</p>

<h2>Part 1: A-Record Configuration</h2>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="A-Record Configuration Image" width="80%">
</p>

<p><strong>Step 1: Connect to the Virtual Machines</strong></p>
<ul>
  <li>Turn on both <strong>DC-1</strong> and <strong>Client-1</strong> in the Azure Portal if they are off.</li>
  <li>Connect to <strong>DC-1</strong> using the domain admin account: <strong>mydomain.com\jane_admin</strong>.</li>
  <li>Connect to <strong>Client-1</strong> using the domain admin account: <strong>mydomain\jane_admin</strong>.</li>
</ul>

<p><strong>Step 2: Testing DNS</strong></p>
<ul>
  <li>On <strong>Client-1</strong>, try to ping the hostname <strong>"mainframe"</strong>. Observe that the ping fails since there is no DNS record for “mainframe”.</li>
  <li>Run <strong>nslookup mainframe</strong> from <strong>Client-1</strong> and observe that it fails because no DNS record exists.</li>
</ul>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="Testing DNS Image" width="80%">
</p>

<p><strong>Step 3: Create a DNS A-Record</strong></p>
<ul>
  <li>On <strong>DC-1</strong>, open the DNS Manager and create a new A-record for <strong>"mainframe"</strong>.</li>
  <li>Set the record to point to <strong>DC-1’s private IP address</strong>.</li>
  <li>Go back to <strong>Client-1</strong> and ping <strong>"mainframe"</strong> again. Observe that the ping now succeeds because of the new A-record.</li>
</ul>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="Create A-Record Image" width="80%">
</p>

<h2>Part 2: Local DNS Cache Management</h2>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="Local DNS Cache Image" width="80%">
</p>

<p><strong>Step 4: Modify the DNS Record</strong></p>
<ul>
  <li>On <strong>DC-1</strong>, change the <strong>mainframe</strong> A-record to point to <strong>8.8.8.8</strong> (Google's DNS).</li>
  <li>Go back to <strong>Client-1</strong> and ping <strong>"mainframe"</strong>. Observe that it still pings the old address, as the local DNS cache has not updated yet.</li>
</ul>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="Modify DNS Record Image" width="80%">
</p>

<p><strong>Step 5: View and Flush the DNS Cache</strong></p>
<ul>
  <li>On <strong>Client-1</strong>, open PowerShell or Command Prompt and run <strong>ipconfig /displaydns</strong>. Observe the DNS cache.</li>
  <li>Flush the DNS cache using <strong>ipconfig /flushdns</strong>.</li>
  <li>Run <strong>ipconfig /displaydns</strong> again to verify that the DNS cache is now empty.</li>
  <li>Attempt to ping <strong>"mainframe"</strong> again. Observe that it now resolves to <strong>8.8.8.8</strong> as the updated DNS record is used.</li>
</ul>

<h2>Part 3: CNAME Record Configuration</h2>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="CNAME Record Configuration Image" width="80%">
</p>

<p><strong>Step 6: Create a CNAME Record</strong></p>
<ul>
  <li>On <strong>DC-1</strong>, create a CNAME record that points the hostname <strong>"search"</strong> to <strong>www.google.com</strong>.</li>
  <li>Go back to <strong>Client-1</strong> and ping <strong>"search"</strong>. Observe the result, which should show Google's IP address as per the CNAME record.</li>
  <li>Run <strong>nslookup search</strong> on <strong>Client-1</strong>. Observe the results showing the CNAME redirection to <strong>www.google.com</strong>.</li>
</ul>

<p align="center">
  <img src="IMAGE_URL_HERE" alt="CNAME Record Image" width="80%">
</p>

<h2>Conclusion</h2>
<p>In this lab, you have successfully implemented advanced DNS configurations in an Active Directory environment. You created A-records and CNAME records, managed DNS settings, and handled local DNS cache. These skills are critical for network management and security operations in real-world IT environments.</p>

<p><strong>Note:</strong> Do not delete the VMs in Azure as they will be used in upcoming labs. If you are done for the day and want to save money, simply <strong>Stop</strong>/turn off the VMs within the Azure Portal.</p>
