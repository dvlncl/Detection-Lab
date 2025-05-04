<h1>SSH Server Setup & Authentication Log Monitoring</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#deploy-server">Step 1: Deploy SSH Server</a></li>
    <li><a href="#connect-ssh">Step 2: Connect to Server</a></li>
    <li><a href="#initial-setup">Step 3: Initial System Setup</a></li>
    <li><a href="#monitor-failures">Step 4: Monitor Failed SSH Logins</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="overview">🐧 Overview</h2>
<ul>
  <li>🚀 Deploy an Ubuntu-based SSH server in the cloud</li>
  <li>🧪 Monitor real-time authentication attempts</li>
  <li>🔎 Use CLI tools to extract failed login attempts and analyze brute force activity</li>
</ul>

<h2 id="deploy-server">🖥️ Step 1: Deploy SSH Server</h2>
<ol>
  <li>Log in to <a href="https://www.vultr.com" target="_blank">vultr.com</a></li>
  <li>Click <strong>Deploy New Server</strong></li>
  <li>Choose:
    <ul>
      <li><strong>Server Type:</strong> Cloud Compute (Shared CPU)</li>
      <li><strong>Region:</strong> Toronto</li>
      <li><strong>OS:</strong> Ubuntu 24.04</li>
      <li><strong>Plan:</strong> 1 vCPU / 1 GB RAM</li>
      <li><strong>Extras:</strong> No backups, no IPv6</li>
      <li><strong>Name:</strong> <code>my-dfir-linux-[yourhandle]</code></li>
    </ul>
  </li>
  <li>Click <strong>Deploy</strong> and wait for <code>Running</code> status</li>
</ol>

<h2 id="connect-ssh">🔐 Step 2: Connect to Server</h2>
<ol>
  <li>Open Terminal or PowerShell</li>
  <li>Run:
    <pre><code>ssh root@your-server-ip</code></pre>
  </li>
  <li>At the fingerprint prompt, type <code>yes</code></li>
  <li>Paste your Vultr console password when prompted</li>
</ol>

<h2 id="initial-setup">📦 Step 3: Initial System Setup</h2>
<ol>
  <li>Update packages:
    <pre><code>apt-get update && apt-get upgrade -y</code></pre>
  </li>
  <li>Navigate to the log directory:
    <pre><code>cd /var/log</code></pre>
  </li>
  <li>List logs and view authentication attempts:
    <pre><code>ls
cat auth.log</code></pre>
  </li>
</ol>

<h2 id="monitor-failures">📊 Step 4: Monitor Failed SSH Logins</h2>
<p>After some time running, your server will log brute-force attempts in <code>auth.log</code>. Filter and analyze them:</p>
<ol>
  <li>Find failed SSH login attempts:
    <pre><code>grep -i failed auth.log</code></pre>
  </li>
  <li>Filter those targeting <code>root</code>:
    <pre><code>grep -i failed auth.log | grep -i root</code></pre>
  </li>
  <li>Extract IP addresses:
    <pre><code>grep -i failed auth.log | grep -i root | cut -d' ' -f9</code></pre>
  </li>
</ol>

<h2 id="conclusion">✅ Conclusion</h2>
<ul>
  <li>You deployed an SSH honeypot on Vultr</li>
  <li>Observed real-world brute-force login attempts</li>
  <li>Used Linux CLI tools to analyze authentication logs</li>
</ul>

<p>Events in <code>/var/log/auth.log</code> represent active brute force scanning behavior seen in the wild.</p>
