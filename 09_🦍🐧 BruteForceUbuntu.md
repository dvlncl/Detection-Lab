<h2>🐧 Setting Up an SSH Server and Monitoring Authentication Logs</h2>

<ul>
  <li>🚀 Deploy an SSH server in the cloud</li>
  <li>🧪 Review real-time authentication logs</li>
  <li>🔎 Extract failed login attempts using CLI tools</li>
</ul>

<hr/>

<h3>🖥️ Deploying the Server</h3>
<ol>
  <li>Go to <a href="https://www.vultr.com" target="_blank">vultr.com</a> and sign in.</li>
  <li>Click <strong>Deploy New Server</strong>.</li>
  <li>Choose the following settings:
    <ul>
      <li><strong>Server Type:</strong> Cloud Compute (Shared CPU)</li>
      <li><strong>Region:</strong> Toronto</li>
      <li><strong>OS:</strong> Ubuntu 24.04</li>
      <li><strong>Plan:</strong> 1 CPU / 1 GB RAM</li>
      <li><strong>Extras:</strong> No backups, no IPv6</li>
      <li><strong>Name:</strong> Format as <code>my-dfir-linux-[yourhandle]</code></li>
    </ul>
  </li>
  <li>Click <strong>Deploy</strong> and wait for the status to become <code>Running</code>.</li>
</ol>

<hr/>

<h3>🔐 Connecting to the Server</h3>
<ol>
  <li>Open PowerShell or Terminal.</li>
  <li>Connect via SSH:
    <pre><code>ssh root@your-server-ip</code></pre>
  </li>
  <li>Type <code>yes</code> at the prompt and enter your root password from the Vultr dashboard.</li>
</ol>

<hr/>

<h3>📦 Initial Setup</h3>
<ol>
  <li>Update your system:
    <pre><code>apt-get update && apt-get upgrade -y</code></pre>
  </li>
  <li>Go to the log directory:
    <pre><code>cd /var/log</code></pre>
  </li>
  <li>List and view logs:
    <pre><code>ls
cat auth.log</code></pre>
  </li>
</ol>

<hr/>

<h3>📊 Filtering Failed SSH Login Attempts</h3>
<p>After letting the server run for a bit, extract login failures:</p>
<ol>
  <li>Find all failed logins:
    <pre><code>grep -i failed auth.log</code></pre>
  </li>
  <li>Filter attempts to root:
    <pre><code>grep -i failed auth.log | grep -i root</code></pre>
  </li>
  <li>Extract just the IP addresses:
    <pre><code>grep -i failed auth.log | grep -i root | cut -d' ' -f9</code></pre>
  </li>
</ol>

<p>This shows real-time brute force attempts targeting your root account.</p>

<hr/>

<h3>✅ Conclusion</h3>
<ul>
  <li>You deployed an SSH honeypot in the cloud</li>
  <li>Observed real-world brute force login attempts</li>
  <li>Used Linux command-line tools to filter and analyze logs</li>
</ul>

<p>What you saw in <code>auth.log</code> are brute force attempts.</p>

