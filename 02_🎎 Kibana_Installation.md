  <h1>📊 Kibana Installation and Configuration</h1>

  <div class="section">
    <h2>🔽 Step 1: Download and Install Kibana</h2>
    <ol>
      <li>Visit <a href="https://www.elastic.co/downloads/kibana" target="_blank">Elastic Downloads - Kibana</a></li>
      <li>Choose <code>.deb (x86_64)</code> version (e.g., 8.15)</li>
      <li>Right click on the button and Copy the download link and run:
        <pre>wget [download-link]</pre>
      </li>
      <li>Install it:
        <pre>dpkg -i kibana-8.x.x-amd64.deb</pre>
      </li>
    </ol>
  </div>

  <div class="section">
    <h2>⚙️ Step 2: Configure Kibana</h2>
    <pre>nano /etc/kibana/kibana.yml</pre>
    <p>Uncomment and edit these lines:</p>
    <pre>
server.port: 5601
server.host: [your-public-IP]</pre>
    <p>Save and exit (Ctrl+X, Y, Enter)</p>
  </div>

  <div class="section">
    <h2>🚀 Step 3: Start Kibana</h2>
    <pre>
systemctl daemon-reload
systemctl enable kibana.service
systemctl start kibana.service
systemctl status kibana.service</pre>
  </div>

  <div class="section">
    <h2>🔐 Step 4: Generate Enrollment Token</h2>
    <pre>
cd /usr/share/elasticsearch/bin
./elasticsearch-create-enrollment-token --scope kibana</pre>
    <p>Copy the token output and save it.</p>
  </div>

  <div class="section">
    <h2>🌐 Step 5: Open Firewall Ports</h2>
    <ul>
      <li>Allow port <code>5601</code> in Vultr firewall (for your IP)</li>
      <li>Also run on VM:
        <pre>ufw allow 5601</pre>
      </li>
    </ul>
  </div>

  <div class="section">
    <h2>🌍 Step 6: Access Kibana in Browser</h2>
    <pre>http://[your-public-IP]:5601</pre>
    <p>Paste the enrollment token when prompted.</p>
  </div>

  <div class="section">
    <h2>🔑 Step 7: Log in and Set Persistent Encryption Keys</h2>
    <ol>
      <li>Log in with:<br>
        <code>Username: elastic</code><br>
        <code>Password: [from Elasticsearch auto config]</code>
      </li>
      <li>To generate persistent keys:
        <pre>
cd /usr/share/kibana/bin
./kibana-encryption-keys generate</pre>
      </li>
      <li>Add them to Kibana keystore:
        <pre>
./kibana-keystore add xpack.encryptedSavedObjects.encryptionKey
./kibana-keystore add xpack.reporting.encryptionKey
./kibana-keystore add xpack.security.encryptionKey</pre>
      </li>
      <li>Restart Kibana:
        <pre>systemctl restart kibana</pre>
      </li>
    </ol>
  </div>


