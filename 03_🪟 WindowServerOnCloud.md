<h1>Windows Server Deployment Lab on Vultr</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#prerequisites">Prerequisites</a></li>
    <li><a href="#deploy">Deploy Windows Server on Vultr</a></li>
    <li><a href="#access">Access the Windows Server</a></li>
    <li><a href="#rdp">Confirm RDP Access</a></li>
    <li><a href="#expose">Expose RDP for Logging (Optional)</a></li>
    <li><a href="#naming">Notes and Naming Convention</a></li>
  </ul>
</nav>

<h2 id="prerequisites">✅ Prerequisites</h2>
<ul>
  <li>Vultr account: <a href="https://www.vultr.com" target="_blank">https://www.vultr.com</a></li>
  <li>Basic understanding of remote desktop (RDP) and VM access</li>
  <li>Windows RDP client (e.g., Remote Desktop Connection on Windows or Microsoft Remote Desktop on macOS)</li>
</ul>

<h2 id="deploy">🌐 Step 1: Deploy Windows Server on Vultr</h2>
<ol>
  <li>Log in to <a href="https://www.vultr.com" target="_blank">vultr.com</a></li>
  <li>Click <strong>Deploy > Deploy New Server</strong></li>
  <li>Choose server type: <code>Cloud Compute (Shared CPU)</code></li>
  <li>Select location: <code>Toronto</code> (or the same as other lab assets)</li>
  <li>Choose OS: <code>Windows Server 2022</code></li>
  <li>Plan: <code>$24/month – 1 vCPU / 2 GB RAM</code></li>
  <li><strong>Do not assign to a VPC</strong> – this will isolate it from internal network logging</li>
  <li>Leave Firewall and IPv6 unchecked</li>
  <li>Set hostname: <code>mydf-win-USERNAME</code> (replace <code>USERNAME</code> with your name or handle)</li>
  <li>Click <strong>Deploy Now</strong></li>
</ol>

<h2 id="access">🖥️ Step 2: Access the Windows Server</h2>
<ol>
  <li>Wait until the server status shows <code>Running</code></li>
  <li>Click <strong>View Console</strong></li>
  <li>In console: click arrow icon → <strong>Show Extra Keys</strong> → <strong>Send Ctrl+Alt+Delete</strong></li>
  <li>Click <strong>Copy Password</strong> in Vultr</li>
  <li>Paste into the password field using the console’s clipboard</li>
  <li>You should now be logged into Windows Server</li>
</ol>

<h2 id="rdp">🔁 Step 3: Confirm RDP Access</h2>
<ol>
  <li>Copy the server’s public IP address from Vultr</li>
  <li>On your machine, open:
    <br><strong>Windows:</strong> <code>🪟 + R → mstsc</code>
    <br><strong>Mac/Linux:</strong> Use Microsoft Remote Desktop client
  </li>
  <li>Paste the public IP and click <strong>Connect</strong></li>
  <li>If successful, you’ll reach the Windows login screen</li>
</ol>

<h2 id="expose">🔓 Step 4: Expose RDP for Logging (Optional)</h2>
<p>Exposing the server publicly will attract brute-force login attempts, useful for log analysis exercises later in the lab.</p>
<ul>
  <li><strong>Do not assign the server to a VPC</strong></li>
  <li><strong>Leave Vultr Firewall Group blank</strong> to allow public RDP access</li>
</ul>

<div class="note" style="border-left: 5px solid #ffc107; padding-left: 10px;">
  ⚠️ Warning: Exposing RDP without a firewall invites real-world attacks. Only do this in safe lab environments.
</div>

<h2 id="naming">📝 Step 5: Notes and Naming Convention</h2>
<ul>
  <li>Name format: <code>mydfir-win-Anyname</code></li>
</ul>
