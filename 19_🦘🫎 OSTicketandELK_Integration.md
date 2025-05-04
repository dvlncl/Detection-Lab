<h1>osTicket Integration with Elastic Stack</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#objective">Objective</a></li>
    <li><a href="#steps">Integration Steps</a></li>
    <li><a href="#security">Security Notes</a></li>
    <li><a href="#summary">Summary of Achievements</a></li>
  </ul>
</nav>

<h2 id="objective">🎯 Objective</h2>
<p>Integrate <strong>osTicket</strong> into your Elastic Stack to automatically create tickets based on generated alerts.</p>

<h2 id="steps">🧭 Integration Steps</h2>
<ol>
  <li>
    <strong>Generate API Key in osTicket:</strong>
    <ul>
      <li>Navigate to <em>Admin &gt; Manage &gt; API</em></li>
      <li>Create new API key using the <strong>private IP</strong> of your ELK server</li>
      <li>Enable <code>Can Create Tickets</code> and save the API key</li>
    </ul>
  </li>

  <li>
    <strong>Enable Elastic Trial Features:</strong>
    <ul>
      <li>In <em>Stack Management &gt; License Management</em>, enable the 30-day trial for webhook capabilities</li>
    </ul>
  </li>

  <li>
    <strong>Create Webhook Connector in Kibana:</strong>
    <ul>
      <li>Go to <em>Stack Management &gt; Connectors &gt; Create Connector</em></li>
      <li>Select <strong>Webhook</strong> and name it <code>osTicket</code></li>
      <li>Set HTTP POST to: <code>http://&lt;osTicket-IP&gt;/upload/api/tickets.xml</code></li>
      <li>Add header: <code>x-api-key: &lt;Your API Key&gt;</code></li>
    </ul>
  </li>

  <li>
    <strong>Prepare Webhook Payload:</strong>
    <ul>
      <li>Use XML payload format from <a href="https://github.com/osTicket/osTicket/blob/develop/setup/doc/api/tickets.md" target="_blank">osTicket GitHub</a></li>
      <li>Customize the subject field as: <code>mydfir-30day-challenge-&lt;your_handle&gt;</code></li>
    </ul>
  </li>

  <li>
    <strong>Test Webhook Connector:</strong>
    <ul>
      <li>If timeout occurs, check that both ELK and osTicket are on the same VPC and using correct private IPs</li>
      <li>Manually assign internal IP if required</li>
    </ul>
  </li>

  <li>
    <strong>Update Connector with Internal IP:</strong>
    <ul>
      <li>Use internal IP (e.g., <code>172.31.X.X</code>) in webhook URL for secure communication</li>
    </ul>
  </li>

  <li>
    <strong>Verify Ticket Creation:</strong>
    <ul>
      <li>Check osTicket Agent Panel for newly created ticket</li>
    </ul>
  </li>
</ol>

<h2 id="security">🔒 Security Notes</h2>
<ul>
  <li>Do not expose osTicket or Elastic endpoints publicly</li>
  <li>Use strong API keys and restrict access via firewall</li>
  <li>Secure endpoints using HTTPS (e.g., Let’s Encrypt)</li>
</ul>

<h2 id="summary">✅ Summary of Achievements</h2>
<ul>
  <li>Elastic Stack deployed and integrated</li>
  <li>Alerts configured for brute force (SSH/RDP)</li>
  <li>Mythic C2 detection setup</li>
  <li>osTicket integrated for automatic ticket generation from alerts</li>
</ul>
