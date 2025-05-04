<h1>RDP Abuse: Detection & Protection</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#what-is-rdp">What is RDP?</a></li>
    <li><a href="#how-abused">How RDP is Abused</a></li>
    <li><a href="#find-rdp">How to Find Exposed RDP Servers</a></li>
    <li><a href="#protect">How to Protect Against RDP Abuse</a></li>
    <li><a href="#recap">Recap</a></li>
  </ul>
</nav>

<h2 id="overview">📺 Overview</h2>
<blockquote>🔐 According to Sophos, RDP abuse was found in over 90% of ransomware breaches in 2023.</blockquote>

<h2 id="what-is-rdp">💡 What is RDP?</h2>
<ul>
  <li><strong>RDP (Remote Desktop Protocol)</strong> allows remote control of Windows systems</li>
  <li>Default port: <code>3389</code></li>
  <li>Used for:
    <ul>
      <li>Remote administration</li>
      <li>Endpoint troubleshooting</li>
      <li>Work-from-home access</li>
    </ul>
  </li>
</ul>

<h2 id="how-abused">⚠️ How RDP is Abused</h2>
<ol>
  <li>Scanning for exposed RDP ports across the internet</li>
  <li>Launching <strong>brute-force attacks</strong> on login screens</li>
  <li>Using <strong>phished credentials</strong> for access</li>
  <li>Executing <strong>lateral movement</strong> after dumping credentials</li>
  <li>Exfiltrating data or deploying ransomware</li>
</ol>

<h2 id="find-rdp">🌐 How to Find Exposed RDP Servers</h2>

<h3>🔍 Using Shodan</h3>
<ol>
  <li>Go to <a href="https://www.shodan.io" target="_blank">shodan.io</a></li>
  <li>Search: <code>port:3389</code></li>
  <li>Review results to see exposed RDP services</li>
</ol>

<h3>🔍 Using Censys</h3>
<ol>
  <li>Visit <a href="https://search.censys.io" target="_blank">censys.io</a></li>
  <li>Search: <code>services.port: 3389</code></li>
  <li>Filter by country, ASN, or organization</li>
</ol>

<blockquote>⚠️ WARNING: Use these tools only for defensive asset auditing. Never attempt unauthorized access.</blockquote>

<h2 id="protect">🛡️ How to Protect Against RDP Abuse</h2>

<h3>🚫 1. Turn it Off</h3>
<ul>
  <li>Disable RDP when not actively used</li>
  <li>Regularly scan your own IPs using Shodan or Censys</li>
</ul>

<h3>🔐 2. Enable MFA</h3>
<ul>
  <li>Enforce multi-factor authentication for all RDP logins</li>
  <li>Blocks access even if credentials are stolen</li>
</ul>

<h3>🌐 3. Restrict Access</h3>
<ul>
  <li>Use firewalls to allow RDP only from known IP addresses</li>
  <li>Consider VPN-only access to internal RDP services</li>
</ul>

<h3>🔑 4. Use Strong Passwords</h3>
<ul>
  <li>Minimum 15+ characters with complexity</li>
  <li>Use PAM systems to rotate and audit privileged credentials</li>
</ul>

<h3>👤 5. Avoid Default Accounts</h3>
<ul>
  <li>Disable built-in admin accounts</li>
  <li>Create renamed, custom admin accounts</li>
</ul>

<blockquote>🧠 Note: Strong passwords and renamed accounts may still be vulnerable to credential stuffing if reused credentials are compromised.</blockquote>

<h2 id="recap">✅ Recap</h2>
<ul>
  <li>❌ Disable RDP when not needed</li>
  <li>✅ Require MFA</li>
  <li>🔒 Restrict RDP access by IP</li>
  <li>🔐 Enforce long, unique passwords</li>
  <li>👤 Replace default admin accounts with custom ones</li>
</ul>
