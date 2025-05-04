<h1>Kibana Deployment Lab on Vultr</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#prerequisites">Prerequisites</a></li>
    <li><a href="#download">Download and Install Kibana</a></li>
    <li><a href="#configure">Configure Kibana</a></li>
    <li><a href="#start">Start Kibana</a></li>
    <li><a href="#enrollment">Generate Enrollment Token</a></li>
    <li><a href="#firewall">Open Firewall Ports</a></li>
    <li><a href="#access">Access Kibana in Browser</a></li>
    <li><a href="#encryption">Set Persistent Encryption Keys</a></li>
  </ul>
</nav>

<h2 id="prerequisites">✅ Prerequisites</h2>
<ul>
  <li>Elasticsearch installed and running on your Vultr VM</li>
  <li>VM running Ubuntu 22.04 LTS</li>
  <li>SSH access to your server</li>
  <li>Ports 5601 (Kibana) open in Vultr firewall</li>
</ul>

<h2 id="download">🔽 Step 1: Download and Install Kibana</h2>
<ol>
  <li>Go to <a href="https://www.elastic.co/downloads/kibana" target="_blank">Elastic Kibana Downloads</a></li>
  <li>Choose the <code>.deb (x86_64)</code> version (e.g., 8.15)</li>
  <li>Right-click the download button and copy the link address</li>
  <li>On your server, run:
    <pre><code>
wget [copied-link]
ls
dpkg -i kibana-8.x.x-amd64.deb
    </code></pre>
  </li>
</ol>

<h2 id="configure">⚙️ Step 2: Configure Kibana</h2>
<pre><code>nano /etc/kibana/kibana.yml</code></pre>
<p>Uncomment and edit the following lines:</p>
<pre><code>
server.port: 5601
server.host: [your-public-IP]
</code></pre>
<p>Save and exit: <code>Ctrl+X → Y → Enter</code></p>

<h2 id="start">🚀 Step 3: Start Kibana</h2>
<pre><code>
systemctl daemon-reload
systemctl enable kibana.service
systemctl start kibana.service
systemctl status kibana.service
</code></pre>
<p>You should see <strong>active (running)</strong> status ✅</p>

<h2 id="enrollment">🔐 Step 4: Generate Enrollment Token</h2>
<pre><code>
cd /usr/share/elasticsearch/bin
./elasticsearch-create-enrollment-token --scope kibana
</code></pre>
<p>📋 Copy and save the generated token securely.</p>

<h2 id="firewall">🌐 Step 5: Open Firewall Ports</h2>
<ol>
  <li>In Vultr: go to <strong>Firewall > Manage > Add Firewall Group</strong></li>
  <li>Allow:
    <ul>
      <li>Port <code>5601</code> from your IP</li>
    </ul>
  </li>
  <li>On your VM, allow UFW access:
    <pre><code>ufw allow 5601</code></pre>
  </li>
</ol>

<h2 id="access">🌍 Step 6: Access Kibana in Browser</h2>
<pre><code>http://[your-public-IP]:5601</code></pre>
<p>Paste the enrollment token when prompted to link Kibana with Elasticsearch.</p>

<h2 id="encryption">🔑 Step 7: Set Persistent Encryption Keys</h2>
<ol>
  <li>Log in using:
    <br><code>Username: elastic</code>
    <br><code>Password: [from Elasticsearch auto config]</code>
  </li>
  <li>Generate encryption keys:
    <pre><code>
cd /usr/share/kibana/bin
./kibana-encryption-keys generate
    </code></pre>
  </li>
  <li>Add keys to the Kibana keystore:
    <pre><code>
./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
./kibana-keystore add xpack.reporting.encryptionKey
./kibana-keystore add xpack.security.encryptionKey
    </code></pre>
  </li>
  <li>Restart Kibana:
    <pre><code>systemctl restart kibana</code></pre>
  </li>
</ol>

<div class="note" style="border-left: 5px solid #dc3545; padding-left: 10px;">
  ⚠️ Avoid exposing Kibana over public IP in production. Use a reverse proxy and restrict access.
</div>
