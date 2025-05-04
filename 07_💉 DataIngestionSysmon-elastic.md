<h1>Ingesting Sysmon & Microsoft Defender Logs into Elasticsearch</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#start-integration">Step 1: Start Integration in Kibana</a></li>
    <li><a href="#add-sysmon">Step 2: Add Sysmon Logs</a></li>
    <li><a href="#add-defender">Step 3: Add Microsoft Defender Logs</a></li>
    <li><a href="#troubleshoot">Troubleshooting Tips</a></li>
    <li><a href="#recap">Recap</a></li>
  </ul>
</nav>

<h2 id="start-integration">✅ Step 1: Start Integration in Kibana</h2>
<ol>
  <li>Log in to your <strong>Elasticsearch/Kibana</strong> instance</li>
  <li>Click <strong>Add Integrations</strong> from the homepage</li>
  <li>Search for <strong>Custom Windows Event Logs</strong> (not Sysmon for Linux)</li>
  <li>Select the <strong>Custom Windows Event Logs</strong> integration</li>
</ol>

<h2 id="add-sysmon">✅ Step 2: Add Sysmon Logs</h2>
<ol>
  <li>Click <strong>Add Custom Windows Event Logs</strong></li>
  <li>Name the integration: <code>my-dfir-win-sysmon</code></li>
  <li>Description: <code>Collect Sysmon logs</code></li>
  <li>Get the Sysmon event channel name:
    <ul>
      <li>RDP into your Windows Server</li>
      <li>Press <code>Windows + R</code> → type <code>eventvwr</code></li>
      <li>Navigate to: <br>
        <code>Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational</code>
      </li>
      <li>Right-click <strong>Operational</strong> → Properties → copy <strong>Full Name</strong></li>
    </ul>
  </li>
  <li>Paste that channel name into Kibana</li>
  <li>Select existing policy (e.g., <code>my-dfir-windows-policy</code>) and save</li>
</ol>

<h2 id="add-defender">✅ Step 3: Add Microsoft Defender Logs</h2>
<ol>
  <li>Repeat the same process as Sysmon</li>
  <li>Name it: <code>my-dfir-win-defender</code></li>
  <li>Description: <code>Collect Defender logs</code></li>
  <li>In Event Viewer, find the Defender <strong>Operational</strong> channel</li>
  <li>Copy and paste its full name into the Kibana form</li>
  <li>Click <strong>Advanced Options</strong> and add important Event IDs:
    <ul>
      <li><code>1116</code> – Malware detected</li>
      <li><code>1117</code> – Protection action taken</li>
      <li><code>50001</code> – Real-time protection disabled</li>
    </ul>
  </li>
</ol>

<h2 id="troubleshoot">⚙️ Troubleshooting Tips</h2>
<ul>
  <li>In Kibana → <strong>Fleet → Agents</strong>, check agent activity</li>
  <li>Restart the Elastic Agent on your Windows Server</li>
  <li>Ensure inbound access on port <code>9200</code> is allowed</li>
  <li>In <strong>Discover</strong>, test queries:
    <ul>
      <li><code>winlog.event_id:1</code> (Sysmon)</li>
      <li><code>winlog.event_id:50001</code> (Defender)</li>
    </ul>
  </li>
  <li>If Elastic Agent stats show <code>N/A</code>, check firewall or connectivity</li>
</ul>

<h2 id="recap">🔄 Recap</h2>
<ul>
  <li>✅ Sysmon and Defender log ingestion added via <strong>Custom Windows Event Logs</strong> integration</li>
  <li>✅ Critical Event IDs filtered for targeted detection</li>
  <li>✅ Connectivity issues resolved via Fleet status and firewall tuning</li>
</ul>
