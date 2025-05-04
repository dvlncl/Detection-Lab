<h1>Fleet Server & Elastic Agent Deployment Lab</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#deploy-fleet-server">Step 1: Deploy Fleet Server VM</a></li>
    <li><a href="#configure-fleet-ui">Step 2: Configure Fleet in Kibana</a></li>
    <li><a href="#install-fleet-server">Step 3: Install Fleet Server</a></li>
    <li><a href="#fix-firewall">Fix Firewall Rules (if needed)</a></li>
    <li><a href="#fix-port">Step 4: Fix Port Configuration in Kibana</a></li>
    <li><a href="#rerun-insecure">Step 5: Re-run Install with --insecure</a></li>
    <li><a href="#windows-agent">Step 6: Install Elastic Agent on Windows Server</a></li>
    <li><a href="#confirm-agent">Step 7: Confirm Agent Enrollment</a></li>
  </ul>
</nav>

<h2 id="deploy-fleet-server">✅ Step 1: Deploy Fleet Server VM</h2>
<ul>
  <li>Create a VM with <strong>Ubuntu 22.04</strong> (1 vCPU, 4 GB RAM)</li>
  <li>Location: <code>Toronto</code>, and enable <strong>VPC 2.0</strong></li>
  <li>Private IP: e.g., <code>172.31.0.4</code>; disable backups and IPv6</li>
  <li>Name the instance <code>my-dfir-fleet-server</code> and deploy</li>
</ul>

<h2 id="configure-fleet-ui">✅ Step 2: Configure Fleet in Kibana</h2>
<ul>
  <li>Open Kibana: <code>http://[ELK-Public-IP]:5601</code></li>
  <li>Navigate to <strong>Fleet</strong> under <strong>Management</strong></li>
  <li>Click <strong>Add Fleet Server</strong> → choose <strong>Quick Start</strong></li>
  <li>Use Fleet server’s public IP and port <code>8220</code> in HTTPS format</li>
  <li>Click <strong>Generate Fleet Server Policy</strong></li>
</ul>

<h2 id="install-fleet-server">✅ Step 3: Install Fleet Server</h2>
<ul>
  <li>SSH into Fleet VM as <code>root</code></li>
  <li>Update the OS:
    <pre><code>apt update && apt upgrade -y</code></pre>
  </li>
  <li>Paste and run the install script from Kibana</li>
  <li>Confirm prompts and complete enrollment</li>
</ul>

<h2 id="fix-firewall">🛠 Fix Firewall Rules (if installation fails)</h2>
<ul>
  <li>On ELK Server:
    <pre><code>sudo ufw allow 9200</code></pre>
  </li>
  <li>On Fleet Server:
    <pre><code>
sudo ufw allow 8220
sudo ufw allow 443
    </code></pre>
  </li>
  <li>Ensure any cloud firewall (e.g., Vultr) allows Fleet Server’s public IP</li>
</ul>

<h2 id="fix-port">✅ Step 4: Fix Port Configuration in Kibana</h2>
<ul>
  <li>Go to <strong>Fleet → Settings</strong></li>
  <li>Edit the URL and change port <code>443</code> → <code>8220</code></li>
  <li>Save and redeploy the Fleet Server configuration</li>
</ul>

<h2 id="rerun-insecure">✅ Step 5: Re-run Fleet Install with <code>--insecure</code> (if needed)</h2>
<ul>
  <li>If you encounter SSL/certificate errors, use:
    <pre><code>
./elastic-agent install \
  --url https://[Fleet-IP]:8220 \
  --enrollment-token [token] \
  --insecure
    </code></pre>
  </li>
  <li>Confirm with <code>Y</code> when prompted</li>
</ul>

<h2 id="windows-agent">✅ Step 6: Install Elastic Agent on Windows Server</h2>
<ul>
  <li>In Kibana → <strong>Fleet → Add agent</strong></li>
  <li>Create a new policy: e.g., <code>my-dfir-windows-policy</code></li>
  <li>Choose <strong>Windows</strong> and copy the install script</li>
  <li>On the Windows Server:
    <ul>
      <li>Open PowerShell as Administrator</li>
      <li>Paste and run the script</li>
      <li>If needed, add <code>--insecure</code> at the end</li>
    </ul>
  </li>
</ul>

<h2 id="confirm-agent">✅ Step 7: Confirm Agent Enrollment</h2>
<ul>
  <li>In Kibana → <strong>Fleet → Agents</strong>, verify the Windows agent is <strong>Connected</strong></li>
  <li>Go to <strong>Discover</strong> and check for logs (e.g., Event ID <code>4625</code>)</li>
</ul>
