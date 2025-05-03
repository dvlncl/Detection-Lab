<h2>📚 Intro</h2>
<ul>
  <li>Goal: Understand Command and Control (C2) concepts, importance, common tools, and introduce the Mythic Framework.</li>
</ul>

<h2>🦠 What Happens When You Execute Malware?</h2>
<ul>
  <li>Malicious executables may run discovery commands like <code>ipconfig</code>, <code>whoami</code>, <code>nslookup</code>, and <code>net user</code>.</li>
  <li>Persistence might be established through service creation or scheduled tasks.</li>
  <li>One common goal: establish a Command and Control (C2) session.</li>
</ul>

<h2>🔗 What is a C2?</h2>
<ul>
  <li>C2 (Command and Control) allows attackers to control compromised machines remotely.</li>
  <li>MITRE ATT&CK Framework defines it as techniques to communicate with controlled systems inside a victim's network.</li>
</ul>

<h2>❓ Why is C2 Important for Attackers?</h2>
<ul>
  <li>It enables attackers to steal credentials, move laterally, extract sensitive data, or deploy ransomware.</li>
  <li>Without persistent access like C2, attackers cannot perform extended operations inside environments.</li>
  <li>18 techniques for C2 establishment are documented in MITRE ATT&CK Framework.</li>
</ul>

<h2>🛠️ Common C2 Tools & Frameworks</h2>
<ul>
  <li><strong>Metasploit</strong> — Popular exploit framework included in Kali Linux, used for vulnerability exploitation and control.</li>
  <li><strong>Cobalt Strike</strong> — Commercial adversary simulation tool often abused by real attackers; detection guides exist (e.g., DFIR Report).</li>
  <li><strong>Sliver</strong> — Open-source C2 developed by Bishop Fox; supports mTLS, HTTP/S, DNS, WireGuard communication.</li>
  <li><strong>Mythic</strong> — The focus of this challenge; an open-source C2 framework using Golang, Docker, and web UI for payload tracking.</li>
</ul>

<h2>🧠 Conclusion</h2>
<ul>
  <li>Command and Control is critical for attacker persistence and control within networks.</li>
  <li>Familiarity with common C2 frameworks (Metasploit, Cobalt Strike, Sliver, Mythic) is essential for SOC analysts.</li>
  
</ul>


