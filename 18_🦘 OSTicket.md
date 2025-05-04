<h1>OSTicket Setup and Integration Lab</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#deploy">Deploy Server on Vultr</a></li>
    <li><a href="#xampp">Install XAMPP</a></li>
    <li><a href="#osticket">Install OSTicket</a></li>
    <li><a href="#access">Access & Use OSTicket</a></li>
    <li><a href="#next">Next Steps</a></li>
    <li><a href="#corrections">Key Corrections & Security Recommendations</a></li>
    <li><a href="#final">Final Notes</a></li>
  </ul>
</nav>

<h2 id="deploy">🛠️ Step 1: Deploy Server on Vultr</h2>
<ol>
  <li>Login to <a href="https://www.vultr.com" target="_blank">Vultr</a> and deploy a new instance.</li>
  <li>Server Type: <code>Cloud Compute (Shared CPU)</code></li>
  <li>OS: <code>Windows Server 2022</code> (⚠️ not ideal – see correction)</li>
  <li>Location: <code>Toronto</code></li>
  <li>Plan: <code>1 CPU, 2 GB RAM</code></li>
  <li>Disable: Backups & IPv6</li>
  <li>Enable: <code>VPC</code> and assign a hostname</li>
  <li>RDP into the server using credentials</li>
</ol>

<p><strong>🛡️ Firewall Setup:</strong> Limit access to ports 80 and 443 to trusted IPs only.</p>

<div class="note" style="border-left: 5px solid #dc3545; padding-left: 10px;">
  ⚠️ Correction: Use <strong>Ubuntu/Linux</strong> instead of Windows. OSTicket requires a LAMP stack.
</div>

<h2 id="xampp">📦 Step 2: Install XAMPP</h2>
<ol>
  <li>Download XAMPP v8.2.2 from <a href="https://www.apachefriends.org" target="_blank">apachefriends.org</a></li>
  <li>Install to <code>C:\xampp</code> and open Control Panel</li>
  <li>Start Apache and MySQL</li>
  <li>Access <code>phpMyAdmin</code> via browser → set password for <code>pma</code> and <code>root</code> users</li>
  <li>Add firewall rules to allow TCP ports 80 and 443</li>
</ol>

<div class="note" style="border-left: 5px solid #ffc107; padding-left: 10px;">
  ⚠️ Tip: Avoid exposing phpMyAdmin to the internet. Use SSH tunnel or VPN.
</div>

<h2 id="osticket">📥 Step 3: Install OSTicket</h2>
<ol>
  <li>Download OSTicket v1.18.1 from <a href="https://osticket.com" target="_blank">osticket.com</a></li>
  <li>Extract to: <code>C:\xampp\htdocs\osticket</code></li>
  <li>Rename <code>ost-sampleconfig.php</code> → <code>ost-config.php</code></li>
  <li>Create MySQL database: <code>my_dfir_30_day_db</code> in phpMyAdmin</li>
  <li>Visit <code>http://&lt;your-ip&gt;/osticket/upload</code> to begin setup</li>
  <li>Use DB credentials (e.g., <code>root/winter2024!</code>) during install</li>
  <li>After setup, reset permissions:
    <pre><code>icacls ost-config.php /reset</code></pre>
  </li>
</ol>

<div class="note" style="border-left: 5px solid #0d6efd; padding-left: 10px;">
  💡 Database must be created manually before installation.
</div>

<h2 id="access">🔐 Step 4: Access & Use OSTicket</h2>
<ol>
  <li>Login at <code>/scp</code> using admin credentials</li>
  <li>Configure Helpdesk settings</li>
  <li>Add agents as needed</li>
  <li>Save URLs and credentials
