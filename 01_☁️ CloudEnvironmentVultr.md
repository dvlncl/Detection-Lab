

  <h1>1. Creating Vultr Account Lab Environment</h1>
  <h1>2. Elastic Search Installation</h1>
  <h2>Deploying Elasticsearch on Vultr</h2>

  <div class="section">
    <h3>✅ Prerequisites</h3>
    <ul>
      <li>Vultr account (<a href="https://www.vultr.com" target="_blank">https://www.vultr.com</a>)</li>
      <li>Basic knowledge of Linux & SSH</li>
      <li>PowerShell or Terminal access</li>
    </ul>
  </div>

  <div class="section">
    <h3>🧩 Step 1: Create a Virtual Private Cloud (VPC)</h3>
    <ol>
      <li>Login to <strong>vultr.com</strong></li>
      <li>Go to <strong>Products > Network > VPC 2.0</strong></li>
      <li>Click <strong>Add VPC</strong></li>
      <li>Select a location (e.g., <code>Toronto</code>)</li>
      <li>Set IP range to <code>172.31.0.0/24</code></li>
      <li>Name it <code>mydef-soc-challenge</code> and click Add</li>
    </ol>
    <div class="note">
      ⚠️ Ensure your VM is deployed in the same region as your VPC.
    </div>
  </div>

  <div class="section">
    <h3>🖥 Step 2: Deploy a Virtual Machine</h3>
    <ol>
      <li>Click <strong>Deploy > Deploy New Server</strong></li>
      <li>Location: <code>Toronto</code></li>
      <li>Image: <code>Ubuntu 22.04 LTS</code></li>
      <li>Plan: <code>4 vCPU / 16 GB RAM</code></li>
      <li>Disable Auto Backups & IPv6</li>
      <li>Attach to VPC: <code>mydef-soc-challenge</code></li>
      <li>Name it <code>mydf-elk</code> and click Deploy</li>
    </ol>
  </div>

  <div class="section">
    <h3>🔐 Step 3: Access the VM via SSH</h3>
    <h4>(Optional) I Use <a href="https://www.bing.com/ck/a?!&&p=638079e16ea246fe80f5af294667cd9d52403565315bfbdba4c3f745a74a2f81JmltdHM9MTc0NTAyMDgwMA&ptn=3&ver=2&hsh=4&fclid=1648ae4e-d8a1-6641-3338-bb19d92d6748&psq=mobaxterm&u=a1aHR0cHM6Ly9tb2JheHRlcm0ubW9iYXRlay5uZXQvZG93bmxvYWQuaHRtbA&ntb=1"> MobaXterm </a> in order for me to properly manage the credentials and remote access </h4></br>
    <pre>ssh root@your-public-ip</pre>
    <p>Accept the prompt and paste the password from the Vultr console.</p>
  </div>

  <div class="section">
    <h3>⬆️ Step 4: Update Packages</h3>
    <pre>apt-get update && apt-get upgrade -y</pre>
  </div>

  <div class="section">
    <h3>📦 Step 5: Install Elasticsearch</h3>
    <ol>
      <li>Go to <a href="https://www.elastic.co/downloads/elasticsearch" target="_blank">Elastic Downloads</a></li>
      <li>Right client on the button and Copy the link address for <code>.deb x86_64</code></li>
      <li>On your server:
        <pre>wget [copied-link]
ls
dpkg -i elasticsearch-8.x.x-amd64.deb</pre>
      </li>
      <li>Save the auto-generated password and token (e.g., in Notepad)</li>
      <li>It looks like this: </li>
      <li><pre>--------------------------- Security autoconfiguration information ------------------------------
      </pre></li>
      <li>If needed, reset with:
        <pre>/usr/share/elasticsearch/bin/elasticsearch-reset-password -u elastic</pre>
      </li>
    </ol>
  </div>

  <div class="section">
    <h3>⚙️ Step 6: Configure Elasticsearch Access</h3>
    <pre>nano /etc/elasticsearch/elasticsearch.yml</pre>
    <p>Update the following:</p>
    <pre>
network.host: ###The Virtual Machine Public IP Address
http.port: 9200
    </pre>
    <p>Find your IP using <code>ip a</code>, then save and exit (<code>Ctrl+X, Y, Enter</code>).</p>
  </div>

  <div class="section">
    <h3>🔒 Step 7: Configure Firewall Rules</h3>
    <ol>
      <li>In Vultr > Firewall > Manage > Add Firewall Group</li>
      <li>Name it <code>30day-mydef-soc-fw</code></li>
      <li>Allow:
        <ul>
          <li>SSH (22) from your IP</li>
          <li>Elasticsearch (9200) from your IP</li>
        </ul>
      </li>
      <li>Apply the firewall group to your VM under <strong>Settings > Firewall</strong></li>
    </ol>
  </div>

  <div class="section">
    <h3>🚀 Step 8: Start Elasticsearch</h3>
    <pre>
systemctl daemon-reload
systemctl enable elasticsearch.service
systemctl start elasticsearch.service
systemctl status elasticsearch.service
    </pre>
    <p>You should see <strong>active (running)</strong> status ✅</p>
  </div>


