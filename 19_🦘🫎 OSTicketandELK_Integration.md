<h2>🦘🫎  osTicket Integration with Elastic</h2>

<h3>🎯 Objective</h3>
<p>Integrate <strong>osTicket</strong> into your Elastic Stack to automatically create tickets from alerts.</p>

<h3>🧭 Steps</h3>

<ol>
<li><strong>Access osTicket Admin Panel:</strong>
<ul>
  <li>Navigate to <em>Admin &gt; Manage &gt; API</em> and create a new API key.</li>
  <li>Use private IP of ELK server if in same VPC.</li>
  <li>Enable <code>Can Create Tickets</code>.</li>
  <li>Save and copy the API key.</li>
</ul>
</li>

<li><strong>Enable Elastic Trial Features:</strong>
<ul>
  <li>Go to <em>Stack Management &gt; License Management</em> and enable the 30-day trial.</li>
</ul>
</li>

<li><strong>Create Elastic Webhook Connector:</strong>
<ul>
  <li>Go to <em>Stack Management &gt; Connectors &gt; Create Connector</em></li>
  <li>Select <strong>Webhook</strong>, name it <em>osTicket</em></li>
  <li>Use HTTP POST to: <code>http://&lt;osTicket-IP&gt;/upload/api/tickets.xml</code></li>
  <li>Add HTTP Header: <code>x-api-key: &lt;Your API Key&gt;</code></li>
</ul>
</li>

<li><strong>Use Payload from osTicket GitHub:</strong>
<ul>
  <li>Paste example XML payload and update the subject to: <code>mydfir-30day-challenge-&lt;your_handle&gt;</code></li>
</ul>
</li>

<li><strong>Test the Webhook:</strong>
<ul>
  <li>If timeout occurs, ensure both ELK and osTicket servers are in same VPC with correct private IPs assigned.</li>
  <li>Manually assign private IP in Control Panel if necessary.</li>
</ul>
</li>

<li><strong>Update Connector:</strong>
<ul>
  <li>Use internal IP (e.g., <code>172.31.X.X</code>) for webhooks within the same network.</li>
  <li>You can find the XML payload here <a href="https://github.com/osTicket/osTicket/blob/develop/setup/doc/api/tickets.md">osTicket Github</a></li>
</ul>
</li>

<li><strong>Verify Success:</strong>
<ul>
  <li>Go to osTicket Agent Panel and confirm ticket creation.</li>
</ul>
</li>
</ol>

<h3>🔒 Security Notes</h3>
<ul>
<li>Do not expose osTicket or Elastic endpoints to the public internet.</li>
<li>Use strong API keys and limit IP access via firewall.</li>
<li>Enable HTTPS (e.g., Let’s Encrypt).</li>
</ul>

<h3>✅ Summary of Achievements</h3>
<ul>
<li>Elastic stack setup with alerts and data ingestion</li>
<li>SSH and RDP brute-force alerting</li>
<li>Mythic C2 detection</li>
<li>osTicket deployment and alert ticketing integration</li>
</ul>
