<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#prerequisites">📋 Prerequisites</a></li>
    <li><a href="#step-1">🔧 Step 1: Add Elastic Defend Integration</a></li>
    <li><a href="#step-2">💽 Step 2: Install and Enroll Elastic Agent</a></li>
    <li><a href="#step-3">🧪 Step 3: Test Malware Detection</a></li>
    <li><a href="#step-4">🔄 Step 4: Configure Automated Response</a></li>
    <li><a href="#step-5">📊 Step 5: Analyze Telemetry</a></li>
  </ul>
</nav>

<h2 id="elastic-defend-setup">🛡️ Elastic Defend Setup Guide</h2>

<h3 id="prerequisites">📋 Prerequisites</h3>
<ul>
  <li>Elastic Stack (Elasticsearch + Kibana) is up and running</li>
  <li>Fleet Server is configured</li>
  <li>Admin access to Kibana</li>
</ul>

<h3 id="step-1">🔧 Step 1: Add Elastic Defend Integration</h3>
<ol>
  <li>Open <strong>Kibana</strong> and click on the ☰ <em>hamburger menu</em></li>
  <li>Go to <strong>Management &gt; Integrations</strong></li>
  <li>Search for <strong>Elastic Defend</strong>, then click <strong>Add</strong></li>
  <li>
    Fill out the form:
    <ul>
      <li><strong>Name:</strong> MyDFIR-EDR</li>
      <li><strong>Description:</strong> Elastic EDR for 30-Day Challenge</li>
      <li><strong>Platform:</strong> Traditional Endpoint</li>
      <li><strong>Configuration:</strong> Complete EDR</li>
    </ul>
  </li>
  <li>Select an Agent Policy (e.g., <code>my-windows-policy</code>)</li>
  <li>Click <strong>Save and continue</strong> &gt; <strong>Save and deploy changes</strong></li>
</ol>

<h3 id="step-2">💽 Step 2: Install and Enroll Elastic Agent</h3>
<ol>
  <li>Go to <strong>Management &gt; Fleet &gt; Agents</strong></li>
  <li>Click <strong>Add Agent</strong>, select the same policy used above</li>
  <li>Follow the installation steps for your platform (e.g., Windows)</li>
  <li>Run the provided command on the endpoint to install and enroll the agent</li>
  <li>Verify enrollment under <strong>Fleet Agents</strong> and <strong>Security &gt; Endpoints</strong></li>
</ol>

<h3 id="step-3">🧪 Step 3: Test Malware Detection</h3>
<ol>
  <li>Attempt to execute a test malware (e.g., <code>mydfir-d30.exe</code>)</li>
  <li>Elastic Defend should:
    <ul>
      <li>Prevent execution</li>
      <li>Quarantine the file</li>
      <li>Generate an alert</li>
    </ul>
  </li>
  <li>View details under <strong>Discover</strong> and <strong>Security &gt; Alerts</strong></li>
</ol>

<h3 id="step-4">🔄 Step 4: Configure Automated Response</h3>
<ol>
  <li>Navigate to <strong>Security &gt; Rules</strong></li>
  <li>Find <code>Malware Prevention Alert</code> &gt; click <strong>Edit Rule Settings</strong></li>
  <li>Under <strong>Actions</strong>:
    <ul>
      <li>Select <strong>Elastic Defend</strong></li>
      <li>Choose <strong>Isolate Host</strong></li>
      <li>Comment: <code>Testing Isolation</code></li>
    </ul>
  </li>
  <li>Save changes</li>
  <li>Trigger the rule again (e.g., re-run the test malware)</li>
  <li>Verify the host is marked as <strong>Isolated</strong> under <strong>Endpoints</strong></li>
</ol>

<h3 id="step-5">📊 Step 5: Analyze Telemetry</h3>
<ul>
  <li>Go to <strong>Security &gt; Alerts</strong></li>
  <li>View:
    <ul>
      <li>Process executable</li>
      <li>File hash</li>
      <li>Quarantine path</li>
      <li>Agent name</li>
    </ul>
  </li>
  <li>Use <strong>Discover</strong> to filter based on <code>event.code: "malicious_file"</code></li>
  <li>Observe the <strong>process tree</strong> if malware spawned additional processes</li>
</ul>
