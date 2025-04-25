<h2>🦆 Installing the Elastic Agent on Your SSH Server</h2>

<ul>
  <li>🔌 Install the Elastic Agent on your Day 12 SSH server</li>
  <li>📥 Forward logs into your Elasticsearch instance</li>
  <li>🕵️ Query authentication logs within Kibana Discover</li>
</ul>

<hr/>

<h3>🧰 Step 1: Create Agent Policy</h3>
<ol>
  <li>Open your Elasticsearch web UI.</li>
  <li>Click the ☰ menu → <strong>Fleet</strong> under <em>Management</em>.</li>
  <li>Select <strong>Agent Policies</strong> → <strong>Create Agent Policy</strong>.</li>
  <li>Name it <code>my-dfir-linux-policy</code>.</li>
  <li>Click <strong>Create Agent Policy</strong>.</li>
</ol>

<hr/>

<h3>📦 Step 2: Add the System Integration</h3>
<ol>
  <li>Open the new policy and add the <strong>System</strong> integration.</li>
  <li>Check the log path; on Ubuntu it should be <code>/var/log/auth.log</code>.</li>
  <li>Note: RedHat/CentOS would use <code>/var/log/secure</code>.</li>
</ol>

<hr/>

<h3>🔗 Step 3: Enroll the SSH Server into Fleet</h3>
<ol>
  <li>Go to <strong>Fleet → Agents</strong> → <strong>Add Agent</strong>.</li>
  <li>Select the <strong>my-dfir-linux-policy</strong>.</li>
  <li>Choose <strong>Enroll in Fleet</strong> → Platform: <strong>Linux TAR</strong>.</li>
  <li>Copy the command provided by Kibana.</li>
  <li>SSH into your Linux server, change to home directory, and run the command.</li>
</ol>

<p><strong>⚠️ Tip:</strong> If you get an <code>x509: certificate signed by unknown authority</code> error, add the <code>--insecure</code> flag to the command and re-run it.</p>

<p><strong>✅ You should now see:</strong> <em>Agent enrollment confirmed</em> in Kibana.</p>

<hr/>

<h3>🔍 Step 4: View Logs in Discover</h3>
<ol>
  <li>Go to the <strong>Discover</strong> section in Kibana.</li>
  <li>Search by <code>agent.name</code> and select your Linux host (e.g., <code>my-dfir-linux-yourhandle</code>).</li>
  <li>To filter for authentication failures, search for <code>message: \"authentication failure\"</code>.</li>
  <li>Add the <code>message</code> field to your table view by toggling its visibility.</li>
</ol>

<hr/>

<h3>📊 Bonus: Investigate IP Address of Attackers</h3>
<ol>
  <li>Back in your SSH server, run:
    <pre><code>cd /var/log
grep -i failed auth.log | grep -i root | cut -d' ' -f9</code></pre>
  </li>
  <li>Copy the IP address and search it in Kibana for all related activity.</li>
</ol>

<hr/>

<h3>✅ Recap</h3>
<ul>
  <li>Elastic Agent was installed and enrolled on your SSH honeypot</li>
  <li>Authentication logs are flowing into Elasticsearch</li>
  <li>You can now search and filter login events in Discover</li>
</ul>
