<h2>🦍 Brute Force Attacks and How to Defend Against Them</h2>

<ul>
  <li>✅ What a brute force attack is</li>
  <li>🛠 Tools attackers use</li>
  <li>🛡️ Techniques to protect yourself and your systems</li>
</ul>

<hr/>

<h3>❓ What is a Brute Force Attack?</h3>
<p>A brute force attack is a method where an attacker attempts to guess a password by trying all possible combinations until the correct one is found. It's like forgetting the lock code on your luggage and testing 0000, 0001, 0002… until it opens. In cybersecurity, attackers use automated tools to do this at scale.</p>
<p>Most systems exposed to the internet — like RDP, SSH, or web portals — are prime targets for brute force attempts.</p>

<hr/>

<h3>📂 Types of Brute Force Attacks</h3>
<ol>
  <li><strong>Simple Brute Force</strong><br>
    Tries every possible character combination until the correct one is found. Time-consuming but effective against short or weak passwords.</li>

  <li><strong>Dictionary Attack</strong><br>
    Uses wordlists containing common passwords, phrases, and leaked credentials. Higher success rate than simple brute force due to reused passwords.</li>

  <li><strong>Credential Stuffing</strong><br>
    Uses real credentials leaked in data breaches. Attackers try known username/password combos on different services — often with great success if users reuse passwords.</li>
</ol>

<hr/>

<h3>🛡️ How to Protect Yourself</h3>
<ol>
  <li><strong>Use Long, Strong Passwords or Passphrases</strong>
    <ul>
      <li>At least 15+ characters</li>
      <li>Include upper/lowercase, numbers, symbols</li>
      <li>Use a <strong>password manager</strong> to generate and store them</li>
      <li>Use easy-to-remember passphrases (e.g., <em>“PleaseSubscribeToMYDFIR”</em>)</li>
    </ul>
  </li>

  <li><strong>Enable Multi-Factor Authentication (MFA)</strong>
    <ul>
      <li>Even if a password is compromised, MFA adds a second verification step</li>
      <li>Use authenticator apps (not SMS or email)</li>
    </ul>
  </li>

  <li><strong>Stay Vigilant</strong>
    <ul>
      <li>Check sender domains and message content in login prompts/emails</li>
      <li>Use <a href="https://haveibeenpwned.com" target="_blank">Have I Been Pwned</a> to check if your credentials have been leaked</li>
      <li>Audit your exposed services (SSH, RDP) and limit public access</li>
    </ul>
  </li>
</ol>

<hr/>

<h3>🧰 Common Brute Force Tools</h3>
<ul>
  <li><strong>Hydra</strong> – Fast and flexible brute force tool</li>
  <li><strong>Hashcat</strong> – GPU-accelerated password cracker</li>
  <li><strong>John the Ripper</strong> – Open-source password testing tool</li>
</ul>
<p>⚠️ <em>Use these tools only in labs or environments you own or have permission to test.</em></p>

<hr/>

<h3>🧠 Recap</h3>
<ul>
  <li>Brute Force = automated password guessing</li>
  <li>Three main types: simple brute force, dictionary, credential stuffing</li>
  <li>Defense includes strong passwords, MFA, and security awareness</li>
  <li>Monitor your infrastructure and reduce public attack surfaces</li>
</ul>

<hr/>

