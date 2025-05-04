<h1>Installing Elastic Agent on SSH Server (Linux Honeypot)</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#create-policy">Step 1: Create Agent Policy</a></li>
    <li><a href="#add-system">Step 2: Add System Integration</a></li>
    <li><a href="#enroll-agent">Step 3: Enroll the SSH Server</a></li>
    <li><a href="#view-logs">Step 4: View Logs in Kibana Discover</a></li>
    <li><a href="#investigate-ip">Bonus: Investigate Attacker IPs</a></li>
    <li><a href="#recap">Recap</a></li>
  </ul>
</nav>

<h2 id="overview">🦆 Overview</h2>
<ul>
  <li>🔌 Install the Elastic Agent on your SSH honeypot (Day 12 server)</li>
  <li>📥 Forward Linux authentication logs into Elasticsearch</li>
  <li>🕵️ Analyze login attempts in Kibana's Discover view</li>
</ul>

<h2 id="create-policy">🧰 Step 1: Create Agent Policy</h2>
<ol>
  <li>Open <strong>Elasticsearch</strong> (Kibana web interface)</li>
  <li>Click the ☰ menu → <strong>Fleet</strong> under <em>Management</em></li>
  <li>Go to <strong>Agent Policies</strong> → click <strong>Create Agent Policy</strong></li>
  <li>Name the policy: <code>my-dfir-linux-policy</code></li>
  <li>Click <strong>Create Agent Policy</strong> to save</li>
</ol>

<h2 id="add-system">📦 Step 2: Add System Integration</h2>
<ol>
  <li>Open the newly created agent policy</li>
  <li>Click <strong>Add Integration</strong> and choose <strong>System</strong></li>
  <li>Ensure log path is correct:
    <ul>
      <li>Ubuntu: <code>/var/log/auth.log</code></li>
      <li>RedHat/CentOS: <code>/var/log/secure</code></li>
    </ul>
  </li>
</ol>

<h2 id="enroll-agent">🔗 Step 3: Enroll the SSH Server</h2>
<ol>
  <li>Go to <strong>Fleet → Agents</strong> → <strong>Add Agent</strong></li>
  <li>Select <code>my-dfir-linux-policy</code> and choose <strong>Enroll in Fleet</strong></li>
  <li>Select platform: <strong>Linux TAR</strong></li>
  <li>Copy the install/enroll command provided by Kibana</li>
  <li>SSH into your server, go to home directory, and paste the command</li>
</ol>

<p><strong>⚠️ Tip:</strong> If you receive an x509 SSL error, re-run the command with <code>--insecure</code></p>
<p><strong>✅ Expected:</strong> You should see “<em>Agent enrolled successfully</em>” in Kibana</p>

<h2 id="view-logs">🔍 Step 4: View Logs in Kibana Discover</h2>
<ol>
  <li>Navigate to <strong>Discover</strong> in Kibana</li>
  <li>Search by:
    <pre><code>agent.name: "my-dfir-linux-yourhandle"</code></pre>
  </li>
  <li>To filter login failures:
    <pre><code>message: "authentication failure"</code></pre>
  </li>
  <li>Toggle the <code>message</code> field to make it visible in the table</li>
</ol>

<h2 id="investigate-ip">📊 Bonus: Investigate Attacker IPs</h2>
<ol>
  <li>On your SSH server, extract failed login IPs:
    <pre><code>
cd /var/log
grep -i failed auth.log | grep -i root | cut -d' ' -f9
    </code></pre>
  </li>
  <li>Copy the IP and paste it into Kibana Discover to pivot and investigate</li>
</ol>

<h2 id="recap">✅ Recap</h2>
<ul>
  <li>Elastic Agent installed and enrolled on your cloud SSH server</li>
  <li>Authentication logs now ingested into Elasticsearch</li>
  <li>Kibana Discover used to investigate brute force attempts</li>
</ul>
