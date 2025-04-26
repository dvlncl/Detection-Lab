<h2> Analyze Windows authentication logs </h2>
<h2> Create a <strong>Brute Force detection alert</strong> for RDP attempts on the Windows server. </h2>
</ul>

<h2>🛠️ Steps & Concepts Covered</h2>

<h3>1. 🧭 Review Windows Authentication Logs</h3>
<ul>
  <li>Access <strong>Discover</strong> in Elastic.</li>
  <li>Set time frame to "Today".</li>
  <li>Filter by agent.name (e.g., <code>mydfir-win-LABNAME</code>).</li>
</ul>

<h3>2. 🔑 Identify Failed Authentication Events</h3>
<ul>
  <li>Search for <strong>Event ID 4625</strong>.</li>
  <li>Use query: <code>event.code:4625</code>.</li>
</ul>

<h3>3. 🧩 Add Relevant Fields to Table</h3>
<ul>
  <li><code>source.ip</code> – IP address of login source.</li>
  <li><code>user.name</code> – Username attempting login.</li>
</ul>

<h3>4. 🕵️ Confirming RDP Relevance</h3>
<ul>
  <li>Check for <strong>logon type 3</strong> in the log message.</li>
  <li>Perform manual failed RDP login and verify logs.</li>
</ul>

<h3>5. ✅ Successful RDP Authentication</h3>
<ul>
  <li><strong>Event ID 4624</strong> = successful login.</li>
  <li><strong>Logon Type 10</strong> = Remote Desktop.</li>
</ul>

<h3>6. 💾 Saving Search</h3>
<ul>
  <li>Save query as <strong>RDP Failed Activity</strong>.</li>
  <li>Ensure both SSH and RDP queries are listed.</li>
</ul>

<h3>7. 🚨 Creating Alerts via Discover</h3>
<ul>
  <li>Go to <strong>Alerts</strong> → <strong>Create search threshold rule</strong>.</li>
  <li>Query: <code>event.code:4625</code>, Threshold: >5 within 5 minutes.</li>
  <li>Include your handle in alert name.</li>
</ul>

<h3>8. 🔐 Creating Detailed Alerts via Detection Rules</h3>
<ul>
  <li>Navigate to <strong>Security</strong> → <strong>Rules</strong> → <strong>Create new rule</strong>.</li>
  <li>Use custom query: <code>event.code:4625 AND user.name:administrator</code>.</li>
  <li>Group by: <code>source.ip</code> and <code>user.name</code>.</li>
  <li>Schedule rule: Run every 1 minute, look back 5 minutes.</li>
  <li>Add rule name, description, fields, and create rule.</li>
</ul>

<h3>9. 🧪 Testing and Alert Insights</h3>
<ul>
  <li>Simulate brute force login to Windows server.</li>
  <li>Verify alert with source IP and username.</li>
  <li>View detailed alert info in Security → Alerts.</li>
</ul>

<h3>10. 📊 Comparison: Discover vs. Detection Rules</h3>
<ul>
  <li>Discover alerts: limited detail.</li>
  <li>Detection rules: comprehensive log metadata.</li>
</ul>

<h3>11. 🧪 Advanced Options</h3>
<ul>
  <li>Try rule types: <strong>event correlation, indicator match, new terms, ES|QL</strong>.</li>
  <li>Add references, false positives, and MITRE tactics in prod.</li>
</ul>

<h3>12. 📌 Key Takeaways</h3>
<ol>
  <li>Identify exposed services like SSH and RDP.</li>
  <li>Use strong passwords + enable MFA.</li>
  <li>Restrict unnecessary access to critical services.</li>
</ol>

<p>✅ You now have two brute force alerts: SSH (Ubuntu) and RDP (Windows).</p>
<p><a href="https://github.com/dvinci200570197/Detection-Lab/blob/main/%F0%9F%94%A2%20LogonType.md">Click Here for the birds eyeview of Logon Types</a></p>

