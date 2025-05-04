  <h1>Elastic Stack + SSH + Fleet Server Troubleshooting Guide</h1>

  <h2>🚨 Common Kibana & Fleet Server Issues</h2>

  <h3>🔥 Kibana Not Loading? "Connection Timed Out"</h3>
  <ul>
    <li>Allow port 5601 in both your Vultr firewall and UFW on the VM:</li>
  </ul>
  <pre><code># Vultr firewall should allow TCP 5601 from your IP

# On the Ubuntu VM:
sudo ufw allow 5601
sudo systemctl restart kibana
</code></pre>

  <h3>🧱 Fleet Server Enrollment Fails (Timeouts, Port Issues)</h3>
  <ul>
    <li>Allow ports <code>8220</code> (Fleet), <code>9200</code> (Elasticsearch), and <code>443</code> (default fallback):</li>
  </ul>
  <pre><code>sudo ufw allow 8220
sudo ufw allow 9200
sudo ufw allow 443</code></pre>

  <h3>🔒 x509 Certificate Signed By Unknown Authority</h3>
  <p>If you’re using self-signed certificates, bypass validation (for testing only):</p>
  <pre><code>elastic-agent enroll --url=https://&lt;ip&gt;:8220 --enrollment-token=&lt;token&gt; --insecure</code></pre>

  <h2>🧹 How to Remove a Fleet Server in Elastic</h2>

  <h4>✅ Option 1: Remove via Kibana UI</h4>
  <ol>
    <li>Go to <code>http://&lt;your-kibana-ip&gt;:5601</code> → <strong>Fleet</strong>.</li>
    <li>Select the agent, click the <strong>⋮</strong> menu → <strong>Unenroll</strong>.</li>
    <li>(Optional) Delete the Fleet Server Policy under <strong>Agent Policies</strong>.</li>
  </ol>

  <h4>✅ Option 2: Remove via CLI</h4>
  <ol>
    <li>SSH into your Fleet Server and run:</li>
  </ol>
  <pre><code>sudo /opt/Elastic/Agent/elastic-agent uninstall</code></pre>

  <h4>✅ Option 3: Manual Cleanup</h4>
  <ul>
    <li>Delete:
      <ul>
        <li><strong>Agents</strong> and <strong>Agent Policies</strong> in Kibana Fleet UI.</li>
      </ul>
    </li>
    <li>Reset the indices (optional):
      <pre><code>DELETE .fleet*
DELETE logs-*
DELETE metrics-*</code></pre>
    </li>
  </ul>

  <h2>🛠 SSH Troubleshooting Commands for Ubuntu</h2>
  <pre><code># 1. Check SSH service status
sudo systemctl status ssh

# 2. Test SSH configuration for syntax errors
sudo sshd -t

# 3. Regenerate missing SSH host keys
sudo ssh-keygen -A

# 4. Reload systemd and restart SSH
sudo systemctl daemon-reexec
sudo systemctl restart ssh

# 5. View detailed SSH logs
journalctl -xeu ssh

# 6. Check if port 22 is already in use
sudo lsof -i :22

# 7. Reinstall SSH server (if needed)
sudo apt purge openssh-server -y
sudo apt install openssh-server -y
sudo ssh-keygen -A
sudo systemctl restart ssh

# 8. Allow SSH through UFW firewall
sudo ufw allow ssh
sudo ufw reload
</code></pre>

  <div class="note">
    💡 <strong>Pro Tip:</strong> Always verify port access using <code>nmap</code> or <code>telnet</code> from another machine.
  </div>
