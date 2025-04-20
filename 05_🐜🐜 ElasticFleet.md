<h3>✅ Step 1: Deploy the Fleet Server</h3>
<ul>
  <li>Create a new VM using <strong>Ubuntu 22.04</strong> (1 CPU, 4 GB RAM).</li>
  <li>Select a location (e.g., <code>Toronto</code>) and enable <strong>VPC 2.0</strong>.</li>
  <li>Assign a private IP (e.g., <code>172.31.0.4</code>) and leave backups/IPv6 disabled.</li>
  <li>Name the server <code>my-dfir-fleet-server</code> and deploy.</li>
</ul>

<h3>✅ Step 2: Configure Fleet in Kibana</h3>
<ul>
  <li>Access Kibana at <code>http://[Public-IP]:5601</code>.</li>
  <li>Go to <strong>Fleet</strong> under the <strong>Management</strong> menu.</li>
  <li>Click <strong>Add Fleet Server</strong> → choose <strong>Quick Start</strong>.</li>
  <li>Provide a name and use the Fleet server’s public IP with port <code>8220</code> in HTTPS format.</li>
  <li>Click <strong>Generate Fleet Server Policy</strong>.</li>
</ul>

<h3>✅ Step 3: Install Fleet Server on Ubuntu</h3>
<ul>
  <li>SSH into the Fleet server as <code>root</code>.</li>
  <li>Update the system:
    <pre><code>apt update &amp;&amp; apt upgrade -y</code></pre>
  </li>
  <li>Paste and run the Fleet install script from Kibana.</li>
  <li>Confirm prompts to complete installation and enrollment.</li>
</ul>

<h3>🛠 If Installation Fails: Fix Firewall Rules</h3>
<ul>
  <li>On ELK server:
    <pre><code>sudo ufw allow 9200</code></pre>
  </li>
  <li>On Fleet server:
    <pre><code>sudo ufw allow 8220
sudo ufw allow 443</code></pre>
  </li>
  <li>Ensure any cloud firewall allows inbound traffic from your Fleet server’s public IP.</li>
</ul>

<h3>✅ Step 4: Fix Port Configuration in Kibana</h3>
<ul>
  <li>Go to <strong>Fleet → Settings</strong> in Kibana.</li>
  <li>Edit the URL and change port <code>443</code> to <code>8220</code>.</li>
  <li>Save and deploy the new configuration.</li>
</ul>

<h3>✅ Step 5: Re-run Fleet Install with --insecure (If Needed)</h3>
<ul>
  <li>If you get a certificate error, re-run with:
    <pre><code>./elastic-agent install --url https://[IP]:8220 --enrollment-token [token] --insecure</code></pre>
  </li>
  <li>Confirm installation with <code>Y</code> and wait for the agent to enroll.</li>
</ul>

<h3>✅ Step 6: Install Elastic Agent on Windows Server</h3>
<ul>
  <li>In Kibana → <strong>Fleet → Add agent</strong>, create a new policy (e.g., <code>my-dfir-windows-policy</code>).</li>
  <li>Select <strong>Windows</strong> and copy the installation script.</li>
  <li>On your Windows Server:
    <ul>
      <li>Open PowerShell as Administrator.</li>
      <li>Paste the script and run it.</li>
      <li>If needed, append <code>--insecure</code> to bypass self-signed certificate issues.</li>
    </ul>
  </li>
</ul>

<h3>✅ Step 7: Confirm Agent Enrollment</h3>
<ul>
  <li>In Kibana → <strong>Fleet → Agents</strong>, verify the new Windows agent appears as connected.</li>
  <li>Go to <strong>Discover</strong> and confirm logs are being ingested (e.g., Event ID <code>4625</code>).</li>
</ul>
