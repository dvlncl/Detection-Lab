<h1>RDP & SSH Brute Force Detection: Demo, Alerts, and Rule Building</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#demo">Demo: Access Discover</a></li>
    <li><a href="#find-failed">Finding Failed Authentications</a></li>
    <li><a href="#create-alert">Creating a Basic Alert</a></li>
    <li><a href="#detection-rule">Building Better Detection Rules</a></li>
    <li><a href="#test">Testing the Rule</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="demo">🖥️ Demo: Access Discover</h2>
<ul>
  <li>Open <strong>Kibana → Discover</strong></li>
  <li>Set the time range to <strong>Today</strong> (~94,000 events)</li>
  <li>Filter logs by <code>agent.name</code> of your RDP host</li>
</ul>

<h2 id="find-failed">🔎 Finding Failed Authentications</h2>
<ul>
  <li>Look for failed logins using:
    <pre><code>event.code:4625</code></pre>
  </li>
  <li>Add table fields:
    <ul>
      <li><code>source.ip</code></li>
      <li><code>user.name</code></li>
    </ul>
  </li>
  <li>Focus on <strong>logon type 3</strong> (network logon via RDP)</li>
  <li>Trigger an RDP login failure manually to generate test data</li>
</ul>

<h2 id="create-alert">🚨 Creating a Basic Alert</h2>
<ul>
  <li>Save the search as: <code>RDP Failed Activity</code></li>
  <li>Go to <strong>Alerts → Create search threshold rule</strong></li>
  <li>Use the saved query: <code>event.code:4625</code></li>
  <li>Threshold: more than 5 events in 5 minutes</li>
  <li>Set alert frequency: every 1 minute</li>
  <li>Save the alert (no action needed for now)</li>
</ul>

<h2 id="detection-rule">🛡️ Building a Better Detection Rule</h2>
<p>For more visibility, use Security → Rules:</p>

<h3>👨‍💻 Create SSH Brute Force Rule</h3>
<ul>
  <li>Go to <strong>Security → Rules → Create new → Threshold rule</strong></li>
  <li>Query:
    <pre><code>event.code:4625 AND user.name:root</code></pre>
  </li>
  <li>Group by: <code>source.ip</code> and <code>user.name</code></li>
  <li>Threshold: >5 failed logins in 5 minutes</li>
  <li>Add: IP, Username, and helpful metadata</li>
  <li>Name the rule: <code>mydfir SSH Brute Force Attempt</code></li>
</ul>

<h3>🧑‍💻 Create RDP Brute Force Rule</h3>
<ul>
  <li>Query:
    <pre><code>event.code:4625 AND user.name:administrator</code></pre>
  </li>
  <li>Group by: <code>source.ip</code> and <code>user.name</code></li>
  <li>Threshold: >5 attempts in 5 minutes</li>
  <li>Name it: <code>mydfir RDP Brute Force Attempt</code></li>
</ul>

<h2 id="test">📈 Testing the Rule</h2>
<ul>
  <li>Simulate a brute-force attack from Kali to your Windows server</li>
  <li>Confirm alert is triggered with:
    <ul>
      <li>Source IP</li>
      <li>Targeted username</li>
      <li>Trigger count</li>
    </ul>
  </li>
  <li>Review the <strong>Insights panel</strong> for context: domain, SID, OS, timestamps</li>
  <li>Note: Some advanced visualizations require an Enterprise license</li>
</ul>

<h2 id="conclusion">🧠 Conclusion</h2>
<ul>
  <li>✅ Basic search alerts offer quick wins</li>
  <li>🛡️ Detailed detection rules provide greater control and visibility</li>
  <li>💡 Use event correlation, indicator match, and ES|QL for advanced logic</li>
  <li>🔒 Harden SSH and RDP exposure: strong passwords, MFA, network restrictions</li>
  <li>🏁 You now have SSH and RDP brute-force detection in place</li>
  <li>📊 Next: Build dashboards to track authentication trends and attack frequency</li>
</ul>
