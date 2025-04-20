<h3>🛠 SSH Troubleshooting Commands for Ubuntu</h3>

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


<h3>🧹 How to Remove a Fleet Server in Elastic</h3>

<h4>✅ Option 1: Remove Fleet Server via Kibana UI</h4>
<ol>
  <li>Go to Kibana at <code>http://&lt;your-kibana-ip&gt;:5601</code>.</li>
  <li>Open the sidebar menu → <strong>Fleet</strong> under <strong>Management</strong>.</li>
  <li>Click on the <strong>"Agents"</strong> tab.</li>
  <li>Locate your <strong>Fleet Server agent</strong>.</li>
  <li>Click the <strong>three-dot menu (⋮)</strong> next to the agent.</li>
  <li>Select <strong>Unenroll agent</strong> and confirm.</li>
  <li>(Optional) Go to <strong>Agent Policies</strong>, select the Fleet Server policy, and <strong>delete</strong> it if not needed.</li>
</ol>

<h4>✅ Option 2: Remove Fleet Server via CLI</h4>
<ol>
  <li>SSH into the server where the Fleet Server is installed.</li>
  <li>Run the following command:
    <pre><code>sudo /opt/Elastic/Agent/elastic-agent uninstall</code></pre>
  </li>
  <li>This will stop, uninstall, and deregister the Elastic Agent.</li>
</ol>

<h4>✅ Option 3: Clean Up Manually (Advanced)</h4>
<ul>
  <li>Delete the Fleet Server host from:
    <ul>
      <li><strong>Kibana → Fleet → Agents</strong></li>
    </ul>
  </li>
  <li>Delete the associated Fleet Server Policy from:
    <ul>
      <li><strong>Kibana → Fleet → Agent policies</strong></li>
    </ul>
  </li>
  <li><strong>(Optional)</strong> Reset the environment by deleting index patterns (only do this if starting over):
    <pre><code>DELETE .fleet*
DELETE logs-*
DELETE metrics-*</code></pre>
  </li>
</ul>

<p>💡 Let me know if you’d like help with any step above or if you’re resetting your whole Elastic environment.</p>

