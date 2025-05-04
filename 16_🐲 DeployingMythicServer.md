<h1>Deploying and Accessing the Mythic C2 Framework</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#demo">Deploy Mythic Server</a></li>
    <li><a href="#setup">Install and Configure Mythic</a></li>
    <li><a href="#secure">Secure the Mythic Server</a></li>
    <li><a href="#access">Access the Mythic Web Interface</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="demo">🖥️ Demo: Deploy Mythic Server</h2>
<ul>
  <li>Deploy a new server on Vultr:
    <ul>
      <li>OS: <code>Ubuntu 22.04</code></li>
      <li>RAM: <code>4GB</code></li>
      <li>Region: <code>Toronto</code></li>
    </ul>
  </li>
  <li>Download Kali Linux locally (VMware preferred)</li>
  <li>SSH into the server:
    <pre><code>ssh root@&lt;server-ip&gt;</code></pre>
  </li>
</ul>

<h2 id="setup">⚙️ Install and Configure Mythic</h2>
<ul>
  <li>Update the server:
    <pre><code>apt-get update && apt-get upgrade -y</code></pre>
  </li>
  <li>Install Docker and Docker Compose:
    <pre><code>apt install make docker-compose -y</code></pre>
  </li>
  <li>Clone Mythic repository:
    <pre><code>git clone https://github.com/its-a-feature/Mythic.git</code></pre>
  </li>
  <li>Navigate to the directory and run setup:
    <pre><code>
cd Mythic
./install_docker_ubuntu.sh
    </code></pre>
  </li>
  <li>If Docker fails to start, run:
    <pre><code>
systemctl restart docker
systemctl status docker
    </code></pre>
  </li>
  <li>Start Mythic services:
    <pre><code>
make
mythic-cli start
    </code></pre>
  </li>
</ul>

<h2 id="secure">🔒 Secure the Mythic Server</h2>
<ul>
  <li>In Vultr, go to <strong>Firewall Groups</strong> and create new rule</li>
  <li>Allow full TCP port range <code>1–65535</code> from:
    <ul>
      <li>Your IP</li>
      <li>Your Kali Linux IP</li>
      <li>Your Windows Server IP</li>
    </ul>
  </li>
  <li>Attach this firewall group to the Mythic server</li>
</ul>

<h2 id="access">🌐 Access the Mythic Web Interface</h2>
<ul>
  <li>Visit:
    <pre><code>https://&lt;server-ip&gt;:7443</code></pre>
  </li>
  <li>If there's an HTTPS error, prepend <code>https://</code> manually in browser</li>
  <li>Find login credentials in:
    <pre><code>
ls -la
cat .env
    </code></pre>
  </li>
  <li>Default username is <code>mythic_admin</code></li>
  <li>Login and explore:
    <ul>
      <li>Payload management</li>
      <li>Callbacks & tasking</li>
      <li>MITRE ATT&CK mappings</li>
      <li>File hosting, tags, CLI support</li>
    </ul>
  </li>
  <li>🌓 Tip: Switch to dark mode with the sun/moon icon in the UI</li>
</ul>

<h2 id="conclusion">🧠 Conclusion</h2>
<ul>
  <li>Mythic provides a powerful red-team C2 interface ideal for SOC defenders to simulate and study attacker behaviors</li>
</ul>
