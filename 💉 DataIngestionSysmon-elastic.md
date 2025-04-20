<h2>💉 Ingesting Sysmon and Microsoft Defender Logs into Elasticsearch</h2>


<hr/>

<h3>✅ Step 1: Start Integration in Kibana</h3>
<ol>
  <li>Log into your Elasticsearch/Kibana instance.</li>
  <li>Click <strong>Add Integrations</strong> on the homepage.</li>
  <li>Search for <strong>Windows Event Logs</strong> (not Sysmon for Linux).</li>
  <li>Select <strong>Custom Windows Event Logs</strong> integration.</li>
</ol>

<h3>✅ Step 2: Add Sysmon Logs</h3>
<ol>
  <li>Click <strong>Add Custom Windows Event Logs</strong>.</li>
  <li>Name it: <code>my-dfir-win-sysmon</code></li>
  <li>Description: <code>Collect Sysmon logs</code></li>
  <li>Find the Sysmon event channel name:
    <ul>
      <li>RDP into your Windows Server</li>
      <li>Open <strong>Event Viewer</strong> → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational</li>
      <li>Right-click <strong>Operational</strong> → Properties → copy <strong>Full Name</strong></li>
    </ul>
  </li>
  <li>Paste that channel name into the integration form in Kibana.</li>
  <li>Select the existing agent policy (e.g., <code>my-dfir-windows-policy</code>) and save.</li>
</ol>

<h3>✅ Step 3: Add Microsoft Defender Logs</h3>
<ol>
  <li>Repeat the process and name it: <code>my-dfir-win-defender</code></li>
  <li>Description: <code>Collect Defender logs</code></li>
  <li>Find the Microsoft Defender Operational channel in Event Viewer.</li>
  <li>Copy and paste its full channel name into Kibana.</li>
  <li>Click <strong>Advanced Options</strong> and include only important Event IDs:
    <ul>
      <li><code>1116</code> – Malware detected</li>
      <li><code>1117</code> – Protection action taken</li>
      <li><code>50001</code> – Real-time protection disabled</li>
    </ul>
  </li>
</ol>

<h3>⚙️ Troubleshooting Tips</h3>
<ul>
  <li>In Kibana, go to <strong>Fleet → Agents</strong> to check last activity.</li>
  <li>Restart the Elastic Agent service on the Windows Server.</li>
  <li>Ensure firewall allows inbound on port <code>9200</code>.</li>
  <li>In <strong>Discover</strong>, search:
    <ul>
      <li><code>winlog.event_id:1</code> (Sysmon)</li>
      <li><code>winlog.event_id:50001</code> (Defender)</li>
    </ul>
  </li>
  <li>If agent stats (CPU/Memory) show <code>N/A</code>, it's likely a connection issue.</li>
</ul>

<h3>🔄 Recap</h3>
<ul>
  <li>Successfully added <strong>Sysmon</strong> and <strong>Microsoft Defender</strong> integrations.</li>
  <li>Filtered useful Event IDs for targeted ingestion.</li>
  <li>Resolved connectivity issues by adjusting firewall rules.</li>
</ul>

