<h1>Elasticsearch Deployment Lab on Vultr</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#prerequisites">Prerequisites</a></li>
    <li><a href="#vpc">Create a Virtual Private Cloud (VPC)</a></li>
    <li><a href="#vm">Deploy a Virtual Machine</a></li>
    <li><a href="#ssh">Access the VM via SSH</a></li>
    <li><a href="#update">Update Packages</a></li>
    <li><a href="#install">Install Elasticsearch</a></li>
    <li><a href="#configure">Configure Elasticsearch Access</a></li>
    <li><a href="#firewall">Configure Firewall Rules</a></li>
    <li><a href="#start">Start Elasticsearch</a></li>
    <li><a href="#verify">Verify Installation</a></li>
  </ul>
</nav>

<h2 id="prerequisites">✅ Prerequisites</h2>
<ul>
  <li>Vultr account: <a href="https://www.vultr.com/?ref=9758799-9J" target="_blank">https://www.vultr.com</a></li>
  <li>Basic knowledge of Linux & SSH</li>
  <li>PowerShell, MobaXterm, or Terminal access</li>
</ul>

<h2 id="vpc">🧩 Step 1: Create a Virtual Private Cloud (VPC)</h2>
<ol>
  <li>Login to <strong>vultr.com</strong></li>
  <li>Go to <strong>Products > Network > VPC 2.0</strong></li>
  <li>Click <strong>Add VPC</strong></li>
  <li>Select a location (e.g., <code>Toronto</code>)</li>
  <li>Set IP range to <code>172.31.0.0/24</code></li>
  <li>Name it <code>mydef-soc-challenge</code> and click Add</li>
</ol>
<div class="note" style="border-left: 5px solid #ffc107; padding-left: 10px;">
  ⚠️ Ensure your VM is deployed in the same region as your VPC.
</div>

<h2 id="vm">🖥 Step 2: Deploy a Virtual Machine</h2>
<ol>
  <li>Click <strong>Deploy > Deploy New Server</strong></li>
  <li>Location: <code>Toronto</code></li>
  <li>Image: <code>Ubuntu 22.04 LTS</code></li>
  <li>Plan: <code>4 vCPU / 16 GB RAM</code></li>
  <li>Disable Auto Backups & IPv6</li>
  <li>Attach to VPC: <code>mydef-soc-challenge</code></li>
  <li>Name it <code>mydf-elk</code> and click Deploy</li>
</ol>

<h2 id="ssh">🔐 Step 3: Access the VM via SSH</h2>
<p><strong>Optional:</strong> Use <a href="https://mobaxterm.mobatek.net/download.html" target="_blank">MobaXterm</a> to simplify SSH access and manage credentials.</p>
<pre><code>ssh root@your-public-ip</code></pre>
<p>Accept the fingerprint prompt and paste the password from the Vultr console.</p>

<h2 id="update">⬆️ Step 4: Update Packages</h2>
<pre><code>apt-get update && apt-get upgrade -y</code></pre>

<h2 id="install">📦 Step 5: Install Elasticsearch</h2>
<ol>
  <li>Go to <a href="https://www.elastic.co/downloads/elasticsearch" target="_blank">Elastic Elasticsearch Downloads</a></li>
  <li>Right-click on the <code>.deb x86_64</code> button and copy the link address</li>
  <li>On your server, run:
    <pre><code>
wget [copied-link]
ls
dpkg -i elasticsearch-8.x.x-amd64.deb
    </code></pre>
  </li>
  <li>Save the auto-generated password and token displayed in the terminal.</li>
  <li>If needed, reset with:
    <pre><code>/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic</code></pre>
  </li>
</ol>

<h2 id="configure">⚙️ Step 6: Configure Elasticsearch Access</h2>
<pre><code>nano /etc/elasticsearch/elasticsearch.yml</code></pre>
<p>Update the following lines:</p>
<pre><code>
network.host: [Your VM's Public IP]
http.port: 9200
</code></pre>
<p>To get your IP: <code>ip a</code></p>
<p>Save and exit: <code>Ctrl+X, Y, Enter</code></p>

<h2 id="firewall">🔒 Step 7: Configure Firewall Rules</h2>
<ol>
  <li>In Vultr: go to <strong>Firewall > Manage > Add Firewall Group</strong></li>
  <li>Name it <code>30day-mydef-soc-fw</code></li>
  <li>Allow:
    <ul>
      <li>SSH (22) from your IP</li>
      <li>Elasticsearch (9200) from your IP</li>
    </ul>
  </li>
  <li>Attach the firewall group to your VM via <strong>Settings > Firewall</strong></li>
</ol>

<h2 id="start">🚀 Step 8: Start Elasticsearch</h2>
<pre><code>
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
systemctl status elasticsearch.service
</code></pre>
<p>You should see <strong>active (running)</strong> status ✅</p>

<h2 id="verify">🔍 Step 9: Verify Installation</h2>
<pre><code>
curl -k -u elastic https://your-public-ip:9200
</code></pre>
<p>If successful, it should return JSON with cluster and node info.</p>

<div class="note" style="border-left: 5px solid #dc3545; padding-left: 10px;">
  ⚠️ Do not expose Elasticsearch on a public IP in production. Use a reverse proxy and secure it properly.
</div>
