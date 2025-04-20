<body>

  <h1>🪟 Windows Server Setup </h1>

  <div class="section">
    <h2>🌐 Step 1: Deploy Windows Server on Vultr</h2>
    <ol>
      <li>Go to <a href="https://www.vultr.com" target="_blank">vultr.com</a> and log in</li>
      <li>Click <strong>Deploy > Deploy New Server</strong></li>
      <li>Server type: <code>Cloud Compute (Shared CPU)</code></li>
      <li>Location: <code>Toronto</code> (or match existing lab)</li>
      <li>Choose <code>Windows Server 2022</code></li>
      <li>Select the <code>$24/month</code> plan (1 vCPU, 2GB RAM)</li>
      <li><strong>Do not select VPC</strong> — keep it isolated from internal lab network</li>
      <li>Leave Firewall and IPv6 <strong>unchecked</strong></li>
      <li>Set the hostname as: <code>mydf-win-USERNAME</code> (replace USERNAME with your own handle)</li>
      <li>Click <strong>Deploy Now</strong></li>
    </ol>
  </div>

  <div class="section">
    <h2>🖥️ Step 2: Access the Windows Server</h2>
    <ol>
      <li>Wait for the server status to show <code>Running</code></li>
      <li>Click <strong>View Console</strong> once available</li>
      <li>Click the arrow icon > <strong>Show Extra Keys</strong> > <strong>Send Ctrl+Alt+Delete</strong></li>
      <li>Click <strong>Copy Password</strong> on Vultr and paste into the password field using the console's clipboard</li>
      <li>You should now be logged into your Windows Server</li>
    </ol>
  </div>

  <div class="section">
    <h2>🔁 Step 3: Confirm RDP Access</h2>
    <ol>
      <li>Copy the server's <strong>public IP address</strong></li>
      <li>Open <strong>Remote Desktop Connection (RDP)</strong> on your local machine or press windows key 🪟 + R and type <u><b>mstsc</b></u>.</li>
      <li>Paste the IP and click <strong>Connect</strong></li>
      <li>If successful, you'll see the Windows login screen</li>
    </ol>
  </div>

  <div class="section">
    <h2>🔓 Step 4: Expose RDP to the Internet (Optional Logging Risk)</h2>
    <p>Leaving the server exposed will result in brute-force attempts, which is useful for learning and logging later in the lab.</p>
    <ul>
      <li><strong>Do not assign the server to the VPC</strong></li>
      <li>Leave the Vultr Firewall Group blank to allow open access</li>
    </ul>
  </div>

  <div class="section">
    <h2>📝 Notes and Naming Convention</h2>
    <ul>
      <li>Name format: <code>mydfir-win-YOURNAME</code></li>
      <li>This helps identify participants for any giveaways or support</li>
    </ul>
  </div>
