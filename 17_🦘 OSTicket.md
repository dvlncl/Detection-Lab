<h2>🦘 OSTicket Setup and Configuration</h2>

<h3>1️⃣ Deploying a Server on Vultr</h3>
<ul>
  <li>🔧 <strong>Steps:</strong>
    <ul>
      <li>Log into Vultr and deploy a new server.</li>
      <li>Select Cloud Compute (Shared CPU), Windows Server 2022 (⚠️ not ideal), and Toronto location.</li>
      <li>Choose Regular Compute (1 CPU, 2GB RAM, 55GB storage).</li>
      <li>Disable Auto-backup & IPv6, enable VPC, and assign hostname.</li>
      <li>RDP into the server using credentials.</li>
    </ul>
  </li>
  <li>🛡️ <strong>Firewall Setup:</strong>
    <ul>
      <li>Add rules to limit access to ports 80 & 443 from trusted IPs only.</li>
    </ul>
  </li>
  <li>⚠️ <strong>Correction:</strong> Use a Linux OS (e.g., Ubuntu) instead of Windows Server. OSTicket requires a LAMP stack.</li>
</ul>

<h3>2️⃣ Installing XAMPP (Web Server)</h3>
<ul>
  <li>📥 Download XAMPP (v8.2.2) from apachefriends.org.</li>
  <li>🛠️ Install it to <code>C:\xampp</code> and open Control Panel.</li>
  <li>📝 Modify Apache domain and phpMyAdmin settings in <code>properties.inc config.inc.php</code>. and make sure you</li>
  <li>🧱 Add Windows Firewall rule for TCP ports 80 and 443.</li>
  <li>▶️ Start Apache and MySQL via XAMPP the go to PHPMyAdmin, add the public IP to accounts[pma and root] then add password</li>
  <li>⚠️ <strong>Security Tip:</strong> Do not expose phpMyAdmin to the public internet. Use SSH tunnel or VPN.</li>
</ul>

<h3>3️⃣ Installing OSTicket</h3>
<ul>
  <li>📦 Download OSTicket (v1.18.1) from osticket.com.</li>
  <li>🗂️ Extract and place contents in <code>C:\xampp\htdocs\osticket</code>.</li>
  <li>🔧 Rename <code>ost-sampleconfig.php</code> to <code>ost-config.php</code>.</li>
  <li>🌐 Access via browser: <code>http://&lt;your-ip&gt;/osticket/upload</code>.</li>
  <li>💾 Create database <code>my_dfir_30_day_db</code> manually in phpMyAdmin.</li>
  <li>🔐 Use root credentials (e.g., winter2024!) to connect database.</li>
  <li>✅ Complete installation and configure admin account.</li>
  <li>🛠️ Reset file permissions via PowerShell: <code>icacls ost-config.php /reset</code>.</li>
  <li>⚠️ <strong>Correction:</strong> The database must be created manually beforehand.</li>
</ul>

<h3>4️⃣ Accessing and Using OSTicket</h3>
<ul>
  <li>🔐 Login to <code>/scp</code> with admin credentials.</li>
  <li>⚙️ Configure Helpdesk settings and add agents as needed.</li>
  <li>📋 Save URLs to Notepad or password manager.</li>
  <li>⚠️ Enable HTTPS and avoid using the root database user in production.</li>
</ul>

<h3>5️⃣ Next Steps</h3>
<ul>
  <li>📡 Integrate OSTicket with your SOC tools to automate alert ticket creation.</li>
</ul>

<h3>🛠️ Key Corrections & Security Recommendations</h3>
<ul>
  <li>❌ <strong>Wrong OS:</strong> Use Linux instead of Windows Server.</li>
  <li>❌ <strong>Public phpMyAdmin:</strong> Bind to 127.0.0.1 and use SSH tunnel.</li>
  <li>❌ <strong>DB Host as Public IP:</strong> Use <code>localhost</code> for DB connections.</li>
  <li>❌ <strong>Weak Credentials:</strong> Use strong, unique passwords. Store securely.</li>
  <li>❌ <strong>Open Firewall Rules:</strong> Limit access by IP ranges.</li>
</ul>

<h3>📝 Final Notes</h3>
<p>OSTicket is now functional, but for production or secure lab use, deploy on Linux, enforce HTTPS, and use strong access controls. Avoid exposing admin panels or phpMyAdmin to the public internet.</p>
