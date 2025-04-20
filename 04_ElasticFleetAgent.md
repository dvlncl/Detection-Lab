<div class="section">
  <h1>🐜 Fleet Server and Elastic Agent</h1>

  <h2>🎯 Why Fleet Server?</h2>
  <p>Imagine installing an agent on 100+ machines and forgetting to enable PowerShell log forwarding. Manually updating every endpoint is inefficient. Instead, a Fleet Server provides a centralized way to manage Elastic Agents, including configuration updates and integration management.</p>
</div>

<div class="section">
  <h2>🔧 What is Elastic Agent?</h2>
  <ul>
    <li>Elastic Agent is a unified way to collect logs, metrics, and security data.</li>
    <li>Uses policies for configuration and integrations.</li>
    <li>Supports standalone or fleet-managed installation.</li>
    <li>Ideal for managing multiple data types from one endpoint.</li>
  </ul>
</div>

<div class="section">
  <h2>📚 Elastic Agent vs Beats</h2>
  <p><strong>Beats:</strong></p>
  <ul>
    <li>Filebeat, Metricbeat, Winlogbeat, Auditbeat, etc.</li>
    <li>Each beat collects specific data type — may need multiple installed on one host.</li>
  </ul>
  <p><strong>Elastic Agent:</strong></p>
  <ul>
    <li>One agent to rule them all — simplifies deployment.</li>
    <li>Can replace multiple Beats.</li>
    <li>Integrates with Fleet for centralized management.</li>
  </ul>
  <p>👉 Elastic Agent is preferred for most modern use cases.</p>
</div>

<div class="section">
  <h2>🌐 What is a Fleet Server?</h2>
  <ul>
    <li>A component that connects Elastic Agents to the Fleet UI.</li>
    <li>Allows for centralized configuration and updates.</li>
    <li>Supports new integrations and uninstallation of agents.</li>
    <li>Makes log routing flexible between Elasticsearch and Logstash.</li>
  </ul>
</div>


