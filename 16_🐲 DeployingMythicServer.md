<h2>🖥️ Demo: Deploying Mythic Server</h2>
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
<pre><code>apt-get update && apt-get upgrade -y
</code></pre>
<ul>
  <li>Install Docker and Docker Compose:</li>
</ul>
<pre><code>apt install make docker-compose -y
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
  <li>Fix Docker service if necessary:</li>
</ul>
<pre><code>systemctl restart docker
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
  <li>Explore Mythic features: payloads, callbacks, tasks, MITRE mapping, tags, file hosting, etc.</li>
  <li>Switch UI to dark mode by clicking the sun/moon icon.</li>
</ul>

<h2>🧠 Conclusion</h2>
<ul>
  <li>Mythic C2 offers a powerful web-based platform for red teaming and SOC defense simulations.</li>
</ul>
