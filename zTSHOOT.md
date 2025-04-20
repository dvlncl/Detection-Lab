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
