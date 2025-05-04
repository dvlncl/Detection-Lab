<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#objective">Objective</a></li>
    <li><a href="#step1">Step 1: Open Security Alerts</a></li>
    <li><a href="#step2">Step 2: Integrate with OS Ticket</a></li>
    <li><a href="#step3">Step 3: Investigative Questions</a></li>
    <li><a href="#step4">Step 4: Post-login Activity</a></li>
    <li><a href="#step5">Step 5: Time Zone and Timeline</a></li>
    <li><a href="#timeline">Example Timeline</a></li>
    <li><a href="#notes">Analyst Notes</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="objective">🔍 Investigating RDP Brute Force Attacks</h2>

<h3>🎯 Objective</h3>
<p>Learn how to investigate an RDP Brute Force alert and analyze potential compromise indicators.</p>

<h3 id="step1">📥 Step 1: Open Security Alerts in Elastic</h3>
<ul>
  <li>Log into Kibana and go to <strong>Security > Alerts</strong>.</li>
  <li>Set the time filter to the last 30 days.</li>
  <li>Filter alerts using the rule name: <strong>RDP Brute Force</strong>.</li>
  <li>Click on an alert to view details like source IP, username (e.g., administrator), and number of events.</li>
</ul>

<h3 id="step2">⚙️ Step 2: Integrate with OS Ticket (Optional)</h3>
<ul>
  <li>Edit the existing RDP Brute Force detection rule.</li>
  <li>Copy the Webhook action body from SSH rule and apply it to the RDP rule.</li>
  <li>Ensure rule schedule is set to run every 1 minute.</li>
</ul>

<h3 id="step3">🔎 Step 3: Investigative Questions</h3>
<ol>
  <li><strong>Is the IP known for brute force?</strong><br>
    - Use tools like <a href="https://www.abuseipdb.com/" target="_blank">AbuseIPDB</a> and <a href="https://viz.greynoise.io/" target="_blank">GreyNoise</a>.
  </li>
  <li><strong>Were other users targeted?</strong><br>
    - Use Discover in Kibana, filter by source IP, and inspect <code>user.name</code> field.
  </li>
  <li><strong>Were there successful logins?</strong><br>
    - Search for <code>event.code:4624</code> from the same IP.</li>
  <li><strong>What activity followed?</strong><br>
    - Use <code>logon.id</code> from the successful login event and search for activity within that session.</li>
</ol>

<h3 id="step4">🕵️‍♂️ Step 4: Analyzing Post-login Activity</h3>
<ul>
  <li>Filter on <code>host.name</code> and <code>user.name</code>.</li>
  <li>Identify <code>logon.id</code> and use it to search for related events.</li>
  <li>Review signs of privilege escalation, command execution, or logoff events.</li>
</ul>

<h3 id="step5">⏱️ Step 5: Time Zone and Timeline</h3>
<ul>
  <li>Go to <strong>Stack Management > Advanced Settings</strong> in Kibana.</li>
  <li>Set time zone to UTC for consistency.</li>
  <li>Create a timeline from first successful login to final logoff for investigation scope.</li>
</ul>

<h3 id="timeline">📌 Example Timeline</h3>
<ul>
  <li><strong>Start:</strong> Aug 12, 2024, 19:56:05 UTC</li>
  <li><strong>End:</strong> Aug 13, 2024, 11:33:40 UTC</li>
</ul>
<table border="1" cellpadding="8" cellspacing="0">
  <thead>
    <tr>
      <th>Investigation Question</th>
      <th>Answer</th>
      <th>How to Investigate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Is this IP known to perform brute force activity?</td>
      <td>✅ Yes (81.163.20.41)</td>
      <td>
        - Query <code>https://www.abuseipdb.com</code> or <code>https://viz.greynoise.io</code><br>
        - Check if the IP has history of brute force, scanning, or malicious behavior<br>
        - Review tags and reports from the platforms
      </td>
    </tr>
    <tr>
      <td>Are any other users affected by this IP?</td>
      <td>❌ No, only Administrator</td>
      <td>
        - Go to Discover in Kibana<br>
        - Set timeframe to 30 days<br>
        - Query: <code>source.ip: "81.163.20.41"</code><br>
        - Add field <code>user.name</code> to the table<br>
        - Check if any usernames other than "Administrator" appear
      </td>
    </tr>
    <tr>
      <td>Were any of the login attempts successful?</td>
      <td>✅ Yes</td>
      <td>
        - Search for successful logins:<br>
        - Query: <code>source.ip: "81.163.20.41" AND event.code: 4624</code><br>
        - Confirm login attempts with <code>event.outcome: success</code> if available
      </td>
    </tr>
    <tr>
      <td>What activity occurred after the successful login?</td>
      <td>
        Session Start:<br> Aug 12, 2024 @ 19:56:05 UTC<br>
        Potential End Time:<br> Aug 13, 2024 @ 01:13:34 UTC
      </td>
      <td>
        - Get <code>logon.id</code> from the 4624 login event<br>
        - Query:<br> 
          <code>winlog.event_data.TargetLogonId: [logon.id]</code><br>
        - Correlate events within the session:<br>
        &emsp;- <code>process.name</code> or <code>process.command_line</code> (process execution)<br>
        &emsp;- <code>file.path</code> (file access/modification)<br>
        &emsp;- <code>destination.ip</code> or <code>network.direction</code> (C2 or lateral movement)<br>
        - Look for 4648 (logon with explicit credentials), 4672 (privileged logon), or 1102 (log cleared)
      </td>
    </tr>
  </tbody>
</table>

<h3 id="notes">🧠 Analyst Notes</h3>
<ul>
  <li>Use Kibana to detect patterns like repeated failed logins or new process creation.</li>
  <li>Look for suspicious activity such as account creation, new services, or exfiltration.</li>
</ul>

<h3 id="conclusion">📢 Conclusion</h3>
<p>RDP Brute Force investigations follow the same methodology as SSH. Use consistent steps, structured queries, and external IP intelligence to validate threats. Continue with the Mythic C2 agent analysis in Day 28.</p>
