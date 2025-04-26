<h2>🖥️ Demo</h2>
<ul>
  <li>Access Elastic Web GUI and select <strong>Discover</strong>.</li>
  <li>Time frame: Set to "Today" (~94,000 events).</li>
  <li>Filter for the RDP server by agent.name.</li>
</ul>

<h2>🔎 Finding Failed Authentications</h2>
<ul>
  <li>Identify Event ID <strong>4625</strong> (failed authentication).</li>
  <li>Use query: <code>event.code:4625</code>.</li>
  <li>Add fields: <code>source.ip</code> and <code>user.name</code>.</li>
  <li>Confirm data by matching logon type 3 (network authentication, RDP).</li>
  <li>Perform manual RDP login attempt to generate test data.</li>
</ul>

<h2>🚨 Creating an Alert</h2>
<ul>
  <li>Save search as <strong>RDP Failed Activity</strong>.</li>
  <li>Go to <strong>Alerts</strong> → Create a <strong>search threshold rule</strong>.</li>
  <li>Query: <code>event.code:4625</code>.</li>
  <li>Threshold: Above 5 failed attempts in 5 minutes.</li>
  <li>Save and monitor for generated alerts.</li>
</ul>

<h2>🛡️ Building a Better Detection Rule</h2>
<ul>
  <li>Alerts created via Discover provide limited information.</li>
  <li>Navigate to <strong>Security → Rules → Create new rule</strong> and select <strong>Threshold rule</strong>.</li>
  <li>Create an SSH brute force rule first:</li>
  <ul>
    <li>Custom query: <code>event.code:4625 AND user.name:root</code>.</li>
    <li>Group by <code>source.ip</code> and <code>user.name</code>.</li>
    <li>Threshold: >5 failed attempts in 5 minutes.</li>
    <li>Add required fields: Source IP and Username.</li>
    <li>Optional: Add setup guides, investigation guides, references, false positive notes, MITRE ATT&CK mappings.</li>
    <li>Name the rule: <strong>mydfir SSH Brute Force Attempt</strong>.</li>
  </ul>
  <li>Then create an RDP brute force rule:</li>
  <ul>
    <li>Custom query: <code>event.code:4625 AND user.name:administrator</code>.</li>
    <li>Group by <code>source.ip</code> and <code>user.name</code>.</li>
    <li>Threshold: >5 failed attempts in 5 minutes.</li>
    <li>Add required fields: Source IP and Username.</li>
    <li>Name the rule: <strong>mydfir RDP Brute Force Attempt</strong>.</li>
  </ul>
  <li>Run both rules every 1 minute with a 5-minute look-back.</li>
</ul>

<h2>📈 Testing the Rule</h2>
<ul>
  <li>Simulate a brute force attack using Kali Linux against the Windows server.</li>
  <li>Confirm alerts are triggered and contain details:</li>
  <ul>
    <li>Source IP address.</li>
    <li>Username involved.</li>
    <li>Threshold counts.</li>
  </ul>
  <li>Insights panel shows additional metadata like SID, domain, OS, first seen, last seen.</li>
  <li>Visualization features require an Enterprise license (not available in basic version).</li>
</ul>

<h2>🧠 Conclusion</h2>
<ul>
  <li>Basic search alerts are good practice, but detailed rules in Security improve visibility dramatically.</li>
  <li>Explore advanced rule types: event correlation, indicator match, new terms, ES|QL.</li>
  <li>Understand exposed assets like SSH and RDP — harden accordingly.</li>
  <li>Use strong passwords, enable MFA, and restrict access as much as possible.</li>
  <li>By now, you have brute force detection for both Ubuntu (SSH) and Windows (RDP) servers.</li>
  <li>Next step: Build dashboards to visualize authentication attempts and threat activity over time.</li>
</ul>
