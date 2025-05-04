<h1>Fleet Server and Elastic Agent Lab Overview</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#why">Why Use Fleet Server?</a></li>
    <li><a href="#agent">What is Elastic Agent?</a></li>
    <li><a href="#comparison">Elastic Agent vs Beats</a></li>
    <li><a href="#fleetserver">What is a Fleet Server?</a></li>
  </ul>
</nav>

<h2 id="why">🎯 Why Use Fleet Server?</h2>
<p>
  Imagine installing an agent on 100+ machines and later realizing you forgot to enable PowerShell log forwarding.  
  Manually updating each endpoint would be inefficient and error-prone.  
  <strong>Fleet Server</strong> solves this by providing centralized control over all Elastic Agents — for updates, policy changes, and integrations.
</p>

<h2 id="agent">🔧 What is Elastic Agent?</h2>
<ul>
  <li>Elastic Agent is a single, unified agent for collecting logs, metrics, and security data.</li>
  <li>Uses **policies** to apply configurations and enable integrations.</li>
  <li>Can run in **standalone mode** or be managed through Fleet.</li>
  <li>Great for environments needing consolidated data collection across endpoints.</li>
</ul>

<h2 id="comparison">📚 Elastic Agent vs Beats</h2>
<p><strong>Beats:</strong></p>
<ul>
  <li>Includes Filebeat, Metricbeat, Winlogbeat, Auditbeat, etc.</li>
  <li>Each Beat is installed separately to collect a specific data type.</li>
  <li>Multiple Beats may need to run on the same host.</li>
</ul>

<p><strong>Elastic Agent:</strong></p>
<ul>
  <li>Consolidated solution — replaces the need for multiple Beats.</li>
  <li>Easier deployment, maintenance, and configuration.</li>
  <li>Integrates seamlessly with the Fleet UI for central management.</li>
</ul>

<p>👉 <strong>Elastic Agent</strong> is the modern, preferred option for most deployment scenarios.</p>

<h2 id="fleetserver">🌐 What is a Fleet Server?</h2>
<ul>
  <li>Fleet Server connects all Elastic Agents to the **Fleet UI** in Kibana.</li>
  <li>It acts as a control plane for centralized configuration and policy management.</li>
  <li>Supports agent updates, integration installs, and removals across systems.</li>
  <li>Can route logs flexibly — either directly to Elasticsearch or via Logstash.</li>
</ul>
