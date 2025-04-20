<h2>Sysmon for Endpoint Visibility</h2>

<h3>🔍 Why Endpoint Visibility Matters</h3>
<p>Having the right visibility into your endpoints is critical for investigation and detection. While Windows does enable basic logging by default, it does not include essential logs such as process creation or network connections. To enhance visibility, analysts can:</p>
<ul>
  <li>Manually configure Windows audit policies</li>
  <li>Or install a tool like <strong>Sysmon</strong> (System Monitor)</li>
</ul>

<h3>✅ What is Sysmon?</h3>
<p>Sysmon is a free tool by Microsoft, part of the Sysinternals Suite. It greatly enhances endpoint telemetry by logging critical system activity like:</p>
<ul>
  <li>Process creations (with command-line, hashes, GUIDs)</li>
  <li>Network connections (source/destination IPs and ports)</li>
  <li>File and driver loads</li>
  <li>Remote thread creations</li>
</ul>
<p>Sysmon is configurable via a custom XML configuration file that controls what events are logged.</p>

<h3>🧠 Key Features of Sysmon</h3>
<ul>
  <li><strong>Process Creation</strong> – Includes parent/child process relationships and command line</li>
  <li><strong>File Hashing</strong> – Logs MD5, SHA1, or SHA256 for binary identification</li>
  <li><strong>Process GUID</strong> – Enables correlation across multiple events for the same process</li>
  <li><strong>Network Monitoring</strong> – Logs source/destination IPs and associated processes (disabled by default)</li>
</ul>

<h3>📌 Recommended Event IDs to Monitor</h3>

<ul>
  <li><strong>Event ID 1 – Process Creation:</strong> Logs new process activity, command-line, file hash, etc.</li>
  <li><strong>Event ID 3 – Network Connection:</strong> Tracks outbound/inbound connections from processes (requires config to enable).</li>
  <li><strong>Event ID 6, 7, 8 – Driver Load, Image Load, Create Remote Thread:</strong> May indicate defense evasion or process injection techniques.</li>
  <li><strong>Event ID 10 – Process Access:</strong> Used to detect access to critical processes like LSASS (often for credential theft).</li>
  <li><strong>Event ID 22 – DNS Query:</strong> Reveals domains being resolved. Useful for spotting DGA-based malware or C2 communications.</li>
  <li><a href="https://github.com/dvinci200570197/Detection-Lab/blob/main/%F0%9F%AA%B5Sysmon.md">Click here for more</a></li>
</ul>

<h3>⚠️ Important Notes</h3>
<ul>
  <li>Events like <strong>3 (Network)</strong> and <strong>7 (Image Load)</strong> are <em>disabled by default</em> and must be enabled in the Sysmon config.</li>
  <li>Some events are noisy and prone to false positives. Use <strong>Process GUID</strong> to correlate events and build accurate timelines.</li>
</ul>

<h3>🧩 Real-World Example</h3>
<p>Imagine an unknown binary is executed from <code>C:\Temp</code>. Sysmon logs this as Event ID 1. Later, the same process opens a suspicious connection — logged as Event ID 3. Both events share the same Process GUID, making it easy to trace the attack path.</p>

<h3>📚 Explore More Event IDs</h3>
<p>Sysmon v15.15 supports 30+ event types. You are encouraged to explore all of them and tailor your configuration to fit your threat model. A full reference link is usually provided in training content or Microsoft's official documentation.</p>

<h3>🎯 What’s Next?</h3>
<p>In the next video, you'll learn how to install Sysmon using a popular community configuration so you can start collecting these powerful logs and apply them in real investigations.</p>

<p>Thank you for following along with Day 8 of the 30-Day DFIR for SOC Analyst Challenge. Stay curious, and do things differently.</p>
