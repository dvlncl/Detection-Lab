<h1>SSH Brute Force Detection & Dashboard Creation</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#overview">Overview</a></li>
    <li><a href="#query-failures">Step 1: Query Failed SSH Logins</a></li>
    <li><a href="#save-search">Step 2: Save the Search</a></li>
    <li><a href="#create-alert">Step 3: Create Brute Force Alert Rule</a></li>
    <li><a href="#build-map">Step 4: Build Kibana Dashboard (Geo Map)</a></li>
    <li><a href="#track-success">Optional: Track Successful Authentications</a></li>
    <li><a href="#recap">Recap</a></li>
  </ul>
</nav>

<h2 id="overview">🗺️ Overview</h2>
<ul>
  <li>🚨 Detect brute-force SSH attacks with alert rules</li>
  <li>🌍 Visualize attacker IP geolocations using Kibana Maps</li>
  <li>🛠️ Query failed logins and build dynamic dashboards</li>
</ul>

<h2 id="query-failures">🔎 Step 1: Query Failed SSH Logins</h2>
<ol>
  <li>Open <strong>Discover</strong> in Kibana</li>
  <li>Filter by your Linux host’s name (e.g., <code>my-dfir-linux-distro</code>)</li>
  <li>Query:
    <pre><code>system.auth.ssh.event: failed</code></pre>
  </li>
  <li>Add the following fields to the table view:
    <ul>
      <li><code>system.auth.ssh.event</code></li>
      <li><code>user.name</code></li>
      <li><code>source.ip</code></li>
      <li><code>source.geo.country_name</code></li>
    </ul>
  </li>
</ol>

<h2 id="save-search">💾 Step 2: Save the Search</h2>
<ol>
  <li>Click <strong>Save</strong> at the top of Discover</li>
  <li>Name it: <code>SSH Failed Activity</code></li>
</ol>

<h2 id="create-alert">🚨 Step 3: Create Brute Force Alert Rule</h2>
<ol>
  <li>Go to <strong>Alerts</strong> → <strong>Create threshold rule</strong></li>
  <li>Rule Name: <code>my-dfir-ssh-brute-force-activity-yourhandle</code></li>
  <li>Use the query from Discover (should be pre-filled)</li>
  <li>Set condition: <strong>Count is above 5 in 5 minutes</strong></li>
  <li>Click <strong>Test query</strong> to preview hits</li>
  <li>Check frequency: every <code>1 minute</code></li>
  <li>Click <strong>Save rule</strong> (alert actions will be configured later)</li>
</ol>

<h2 id="build-map">🗺️ Step 4: Build Kibana Dashboard (Geo Map)</h2>
<ol>
  <li>Go to <strong>Maps</strong> under <em>Analytics</em></li>
  <li>Paste your KQL query from the saved search</li>
  <li>Click <strong>Add Layer</strong> → <strong>Choropleth Layer</strong></li>
  <li>Choose <strong>World Countries</strong> → use field: <code>source.geo.country_iso_code</code></li>
  <li>Select your data view or index pattern</li>
  <li>Save map as: <strong>SSH Network Map</strong></li>
  <li>Add it to a new dashboard titled: <strong>SSH Authentication Activity</strong></li>
</ol>

<h2 id="track-success">✅ Optional: Track Successful Authentications</h2>
<ol>
  <li>Duplicate the saved failed login search</li>
  <li>Change query to:
    <pre><code>system.auth.ssh.event: accepted</code></pre>
  </li>
  <li>Save as: <code>SSH Successful Authentication</code></li>
  <li>Add both saved searches to your dashboard side-by-side</li>
</ol>

<h2 id="recap">🎉 Recap</h2>
<ul>
  <li>🔐 You now have alerting for SSH brute-force attempts</li>
  <li>🗺️ Kibana Maps visualizes attacker geolocation data</li>
  <li>📈 Dashboard shows real-time activity and authentication trends</li>
</ul>
