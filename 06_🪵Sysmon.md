<h1>Sysmon for Endpoint Visibility Lab</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#importance">Why Endpoint Visibility Matters</a></li>
    <li><a href="#what-is-sysmon">What is Sysmon?</a></li>
    <li><a href="#key-features">Key Features of Sysmon</a></li>
    <li><a href="#event-ids">Recommended Event IDs</a></li>
    <li><a href="#notes">Important Notes</a></li>
    <li><a href="#example">Real-World Example</a></li>
    <li><a href="#more-events">Explore More Event IDs</a></li>
  </ul>
</nav>

<h2 id="importance">🔍 Why Endpoint Visibility Matters</h2>
<p>Basic Windows logging does not include vital events like process creation or network activity. To gain deeper visibility for detection and investigation, analysts should:</p>
<ul>
  <li>Manually configure Windows Audit Policies</li>
  <li>Or install <strong>Sysmon</strong> (System Monitor) for enhanced telemetry</li>
</ul>

<h2 id="what-is-sysmon">✅ What is Sysmon?</h2>
<p>
  <strong>Sysmon</strong> is a free Windows system monitoring tool from Microsoft’s Sysinternals Suite.  
  It enhances endpoint visibility by logging:
</p>
<ul>
  <li>Process creations (with command-line, hashes, GUIDs)</li>
  <li>Network connections (IP/port-level logging)</li>
  <li>Driver and image loads</li>
  <li>Remote thread creation and inter-process access</li>
</ul>
<p>Sysmon is configured with a custom XML file to control which events are logged.</p>

<h2 id="key-features">🧠 Key Features of Sysmon</h2>
<ul>
  <li><strong>Process Creation</strong> – Captures command-line args, parent process, and user</li>
  <li><strong>File Hashing</strong> – Generates hashes (MD5, SHA1, SHA256) to identify executables</li>
  <li><strong>Process GUID</strong> – Tracks activities of the same process across different logs</li>
  <li><strong>Network Monitoring</strong> – Logs source/destination IPs + ports (must be enabled)</li>
</ul>

<h2 id="event-ids">📌 Recommended Event IDs to Monitor</h2>
<ul>
  <li><strong>Event ID 1 – Process Creation:</strong> Logs command-line, file hash, user context</li>
  <li><strong>Event ID 3 – Network Connection:</strong> Records process-level TCP/UDP connections (must enable)</li>
  <li><strong>Event IDs 6, 7, 8:</strong> Driver Load, Image Load, Create Remote Thread – often signal stealth or injection</li>
  <li><strong>Event ID 10 – Process Access:</strong> Flags access to sensitive processes like LSASS</li>
  <li><strong>Event ID 22 – DNS Query:</strong> Monitors domain lookups — helps detect DGA/C2 activity</li>
  <li><a href="https://github.com/dvinci200570197/Detection-Lab/blob/main/%F0%9F%AA%B5Sysmon.md" target="_blank">📎 View Sample Config & Full Event Reference</a></li>
</ul>

<h2 id="notes">⚠️ Important Notes</h2>
<ul>
  <li>Events like <strong>3 (Network)</strong> and <strong>7 (Image Load)</strong> are <em>disabled by default</em> and must be enabled in the Sysmon config.</li>
  <li>Some events can be noisy — use <strong>Process GUID</strong> to correlate them into coherent timelines.</li>
</ul>

<h2 id="example">🧩 Real-World Example</h2>
<p>
  Suppose a suspicious binary runs from <code>C:\Temp</code> — Sysmon logs it under Event ID 1.  
  Moments later, it creates an outbound connection — logged as Event ID 3.  
  Both share the same <strong>Process GUID</strong>, helping analysts trace its full behavior easily.
</p>

<h2 id="more-events">📚 Explore More Event IDs</h2>
<p>
  Sysmon (v15.15+) supports over 30 unique event types.  
  You’re encouraged to review the full list and tailor the configuration to your organization's threat model.  
  Visit the official Microsoft Docs or training repositories for detailed schemas.
</p>
