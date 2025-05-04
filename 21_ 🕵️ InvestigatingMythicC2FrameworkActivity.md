<h1>Day 28 - Mythic C2 Detection via Sysmon and Elastic</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#goals">Investigation Goals</a></li>
    <li><a href="#indicators">Initial Indicators</a></li>
    <li><a href="#timeline">Key Events Timeline</a></li>
    <li><a href="#strategy">Detection Strategy</a></li>
    <li><a href="#tips">Analyst Tips</a></li>
    <li><a href="#takeaways">Takeaways</a></li>
  </ul>
</nav>

<h2 id="goals">🕵️ Investigating Mythic C2 Framework Activity</h2>

<h3>🎯 Investigation Goals</h3>
<ul>
  <li>Detect the presence of a C2 agent (<code>Mythic</code>)</li>
  <li>Analyze how it was dropped, executed, and communicated with the attacker</li>
  <li>Correlate <code>Sysmon</code> events using <strong>process.guid</strong></li>
  <li>Highlight importance of endpoint and network telemetry</li>
</ul>

<h2 id="indicators">🚩 Initial Indicators</h2>
<ul>
  <li>C2 Agent: <code>servicehost-handlename.exe</code></li>
  <li>Suspicious path: <code>C:\Users\Public\Downloads</code></li>
  <li>Outbound traffic to Port <code>80</code> and <code>9999</code></li>
</ul>

<h2 id="timeline">🗓️ Key Events Timeline</h2>
<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>Time (UTC)</th>
      <th>Event</th>
      <th>Sysmon Code</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Aug 12, 20:30</td>
      <td>PowerShell Launch</td>
      <td>1</td>
      <td>Administrator launches PowerShell via Explorer</td>
    </tr>
    <tr>
      <td>Aug 12, 20:42:44</td>
      <td>File Created</td>
      <td>11</td>
      <td><code>servicehost-dstepenrocks.exe</code> created via PowerShell</td>
    </tr>
    <tr>
      <td>Aug 12, 20:42–20:53</td>
      <td>Network Connections</td>
      <td>3</td>
      <td>Outbound connection to suspicious IP</td>
    </tr>
    <tr>
      <td>Aug 12, ~20:44</td>
      <td>Executable Detected</td>
      <td>29</td>
      <td>Sysmon detects new executable drop</td>
    </tr>
    <tr>
      <td>Aug 12, ~20:47</td>
      <td>Process Created</td>
      <td>1</td>
      <td>C2 agent executed</td>
    </tr>
    <tr>
      <td>Aug 15, 01:22</td>
      <td>Command Executed: <code>netstat</code></td>
      <td>1</td>
      <td>Triggered from C2 session</td>
    </tr>
    <tr>
      <td>Aug 15, 01:28</td>
      <td>Command Executed: <code>ipconfig</code></td>
      <td>1</td>
      <td>Captured by Sysmon as new cmd session</td>
    </tr>
    <tr>
      <td>Aug 15</td>
      <td>Malware Detected</td>
      <td>—</td>
      <td>Windows Defender flagged Mythic agent</td>
    </tr>
  </tbody>
</table>

<h2 id="strategy">🔍 Detection Strategy</h2>
<ul>
  <li>Pivoted using <code>process.guid</code> for event correlation</li>
  <li>Cross-referenced Event IDs 1, 3, 11, and 29 from Sysmon</li>
  <li>Used Elastic detection rules with OS Ticket webhook for alerting</li>
</ul>

<h2 id="tips">💡 Analyst Tips</h2>
<ul>
  <li>Always monitor both endpoint and network telemetry</li>
  <li>Be alert to unexpected binaries in <code>Public\Downloads</code></li>
  <li>Use dashboards to track PowerShell, RunDLL32, and suspicious ports</li>
</ul>

<h2 id="takeaways">📎 Takeaways</h2>
<ul>
  <li>Mythic C2 agents can be caught using endpoint logs, if well instrumented</li>
  <li>Even stealthy malware leaves behind process and file traces</li>
  <li>Good logging + good pivoting = faster root cause analysis</li>
</ul>
