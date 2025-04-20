<h2>🖥️ Day 15 – RDP Abuse: Detection & Protection</h2>

<p>Welcome to Day 15 of the 30-Day MYDFIR SOC Analyst Challenge! Today, we explore one of the most abused protocols in cybersecurity incidents: <strong>Remote Desktop Protocol (RDP)</strong>.</p>

<blockquote>🔐 According to Sophos, RDP abuse was found in over 90% of ransomware breaches in 2023.</blockquote>

<hr/>

<h3>💡 What is RDP?</h3>
<ul>
  <li><strong>RDP (Remote Desktop Protocol)</strong> is a Microsoft protocol that enables users to remotely access and manage computers.</li>
  <li>It uses <strong>TCP port 3389</strong> by default.</li>
  <li>Commonly used for:
    <ul>
      <li>Remote administration</li>
      <li>Troubleshooting endpoints</li>
      <li>Accessing office systems from home or abroad</li>
    </ul>
  </li>
</ul>

<h3>⚠️ How RDP Gets Abused</h3>
<p>Attackers often abuse RDP by:</p>
<ol>
  <li>Scanning for exposed RDP services over the internet</li>
  <li>Attempting <strong>brute force attacks</strong> (guessing passwords)</li>
  <li>Using <strong>valid credentials</strong> acquired via phishing</li>
  <li>Performing <strong>credential dumping</strong> and moving laterally using RDP</li>
</ol>

<p>Eventually, attackers may exfiltrate data or deploy ransomware.</p>

<hr/>

<h3>🌐 How to Find Exposed RDP Servers</h3>

<h4>🔍 Shodan</h4>
<ol>
  <li>Visit <a href="https://www.shodan.io" target="_blank">shodan.io</a></li>
  <li>Search: <code>port:3389</code></li>
  <li>Review public IPs exposing RDP</li>
</ol>

<h4>🔍 Censys</h4>
<ol>
  <li>Visit <a href="https://search.censys.io" target="_blank">censys.io</a></li>
  <li>Search: <code>services.port: 3389</code></li>
  <li>Filter by country, organization, or IP ranges</li>
</ol>

<blockquote>⚠️ WARNING: Never attempt unauthorized access to discovered IPs. Use this for threat hunting or asset exposure audits only.</blockquote>

<hr/>

<h3>🛡️ How to Protect Against RDP Abuse</h3>
<p>Here are 5 practical recommendations:</p>

<h4>1. 🚫 Turn it Off</h4>
<ul>
  <li>Disable RDP when not in use, especially on dev/test servers.</li>
  <li>Regularly audit exposed services via Shodan/Censys.</li>
</ul>

<h4>2. 🔐 Enable MFA</h4>
<ul>
  <li>Add multi-factor authentication to all RDP sessions where possible.</li>
  <li>Prevents access even if credentials are compromised.</li>
</ul>

<h4>3. 🌐 Restrict Access</h4>
<ul>
  <li>Use firewalls or security groups to allow RDP only from specific IP ranges.</li>
  <li>Preferably place RDP behind a VPN.</li>
</ul>

<h4>4. 🔑 Use Strong Passwords</h4>
<ul>
  <li>Minimum 15+ characters with complexity.</li>
  <li>Consider a <strong>Privileged Access Management (PAM)</strong> system to rotate credentials.</li>
</ul>

<h4>5. 🧑‍💻 Avoid Default Accounts</h4>
<ul>
  <li>Disable built-in local admin accounts.</li>
  <li>Create named admin accounts with custom names.</li>
</ul>

<blockquote>🧠 Note: Points 4 and 5 are less effective against <strong>credential stuffing</strong> (where stolen credentials from breaches are reused).</blockquote>

<hr/>

<h3>✅ Recap</h3>
<ul>
  <li>❌ Turn off RDP when not needed</li>
  <li>✅ Use MFA</li>
  <li>🔒 Restrict access</li>
  <li>🔐 Use strong, unique passwords</li>
  <li>👤 Avoid default accounts</li>
</ul>
