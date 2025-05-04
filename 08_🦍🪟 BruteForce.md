<h1>Brute Force Attacks and How to Defend Against Them</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#what-is">What is a Brute Force Attack?</a></li>
    <li><a href="#types">Types of Brute Force Attacks</a></li>
    <li><a href="#protection">How to Protect Yourself</a></li>
    <li><a href="#tools">Common Brute Force Tools</a></li>
    <li><a href="#recap">Recap</a></li>
  </ul>
</nav>

<h2 id="overview">🦍 Overview</h2>
<ul>
  <li>✅ Understand what a brute force attack is</li>
  <li>🛠 Identify tools used by attackers</li>
  <li>🛡️ Learn techniques to defend your systems</li>
</ul>

<h2 id="what-is">❓ What is a Brute Force Attack?</h2>
<p>A brute force attack is a password-guessing technique where attackers try every possible combination until they succeed. Think of it like testing every combo on a luggage lock: 0000, 0001, 0002... until it opens.</p>
<p>Automated tools make this easy to scale against online services like RDP, SSH, or web login portals.</p>

<h2 id="types">📂 Types of Brute Force Attacks</h2>
<ol>
  <li><strong>Simple Brute Force</strong><br>
  Exhaustively tries all character combinations. Slow, but works on weak passwords.</li>

  <li><strong>Dictionary Attack</strong><br>
  Uses curated lists of common or leaked passwords. Fast and effective against reused credentials.</li>

  <li><strong>Credential Stuffing</strong><br>
  Uses actual breached credentials. Tries known username/password pairs across multiple platforms.</li>
</ol>

<h2 id="protection">🛡️ How to Protect Yourself</h2>
<ol>
  <li><strong>Use Strong Passwords/Passphrases</strong>
    <ul>
      <li>At least 15 characters long</li>
      <li>Mix of uppercase, lowercase, numbers, and symbols</li>
      <li>Use a <strong>password manager</strong> for storage and generation</li>
      <li>Memorable passphrases like <code>PleaseSubscribeToMYDFIR</code></li>
    </ul>
  </li>

  <li><strong>Enable Multi-Factor Authentication (MFA)</strong>
    <ul>
      <li>Adds a second layer even if a password is stolen</li>
      <li>Prefer authenticator apps over SMS or email</li>
    </ul>
  </li>

  <li><strong>Stay Vigilant</strong>
    <ul>
      <li>Inspect sender emails and login prompts</li>
      <li>Use <a href="https://haveibeenpwned.com" target="_blank">Have I Been Pwned</a> to check for leaked credentials</li>
      <li>Audit public-facing services (e.g., RDP, SSH) regularly</li>
    </ul>
  </li>
</ol>

<h2 id="tools">🧰 Common Brute Force Tools</h2>
<ul>
  <li><strong>Hydra</strong> – Fast, flexible network logon cracker</li>
  <li><strong>Hashcat</strong> – Powerful GPU-accelerated password cracker</li>
  <li><strong>John the Ripper</strong> – Popular open-source password testing tool</li>
</ul>
<p>⚠️ <em>These tools should only be used in lab environments or systems you have explicit permission to test.</em></p>

<h2 id="recap">🧠 Recap</h2>
<ul>
  <li>Brute Force = automated trial-and-error password guessing</li>
  <li>Common types include simple, dictionary, and credential stuffing attacks</li>
  <li>Defense relies on strong passwords, MFA, and endpoint hardening</li>
  <li>Continuously monitor and minimize exposed services on the internet</li>
</ul>
