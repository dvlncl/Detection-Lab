<h1>Intro to Command and Control (C2) and the Mythic Framework</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#intro">Introduction</a></li>
    <li><a href="#malware-execution">What Happens When You Execute Malware?</a></li>
    <li><a href="#what-is-c2">What is Command & Control (C2)?</a></li>
    <li><a href="#importance">Why C2 is Important for Attackers</a></li>
    <li><a href="#c2-tools">Common C2 Tools & Frameworks</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="intro">📚 Introduction</h2>
<ul>
  <li>🎯 Goal: Understand Command and Control (C2) concepts, use cases, popular tools, and the Mythic framework</li>
</ul>

<h2 id="malware-execution">🦠 What Happens When You Execute Malware?</h2>
<ul>
  <li>Malware often runs discovery commands:
    <pre><code>ipconfig, whoami, nslookup, net user</code></pre>
  </li>
  <li>May create scheduled tasks or services to gain persistence</li>
  <li>Usually aims to establish a persistent Command and Control session</li>
</ul>

<h2 id="what-is-c2">🔗 What is Command & Control (C2)?</h2>
<ul>
  <li>C2 = attacker’s remote access channel into the victim's machine</li>
  <li>Allows issuing of commands, receiving outputs, deploying payloads</li>
  <li>MITRE defines C2 as techniques used to communicate with infected hosts</li>
</ul>

<h2 id="importance">❓ Why is C2 Important for Attackers?</h2>
<ul>
  <li>Facilitates long-term access inside networks</li>
  <li>Used to steal credentials, move laterally, exfiltrate data, or deploy ransomware</li>
  <li>Without C2, attackers lose control after reboot/logoff</li>
  <li>18 C2-related techniques are listed in the MITRE ATT&CK Matrix</li>
</ul>

<h2 id="c2-tools">🛠️ Common C2 Tools & Frameworks</h2>
<ul>
  <li><strong>Metasploit</strong>: Built-in Kali Linux framework for exploitation and C2</li>
  <li><strong>Cobalt Strike</strong>: Commercial red team tool, commonly abused by threat actors</li>
  <li><strong>Sliver</strong>: Open-source C2 that supports mTLS, DNS, WireGuard, etc.</li>
  <li><strong>Mythic</strong>: Modern, open-source Golang/Docker-based C2 with web UI and payload visibility</li>
</ul>

<h2 id="conclusion">🧠 Conclusion</h2>
<ul>
  <li>Understanding C2 is crucial for effective threat detection and incident response</li>
  <li>SOC analysts should be familiar with how common C2 frameworks work and how to detect them</li>
</ul>
