<h2>🗺️ Creating SSH Brute Force Alerts and Dashboards</h2>

<ul>
  <li>🚨 Create an alert for SSH brute force activity</li>
  <li>🌍 Build a Kibana dashboard to visualize attacker geolocations</li>
  <li>🛠️ Learn how to query failed logins and generate saved searches</li>
</ul>

<hr/>

<h3>🔎 Step 1: Query for Failed SSH Authentications</h3>
<ol>
  <li>Go to <strong>Discover</strong> in Kibana.</li>
  <li>Filter by your Linux host’s agent name (e.g., <code>my-dfir-linux-distro</code>).</li>
  <li>Search for events with SSH login attempts using field <code>system.auth.ssh.event</code>.</li>
  <li>Add the following columns:
    <ul>
      <li><code>system.auth.ssh.event</code></li>
      <li><code>user.name</code></li>
      <li><code>source.ip</code></li>
      <li><code>source.geo.country_name</code></li>
    </ul>
  </li>
  <li>Use the query <code>system.auth.ssh.event: failed</code> to isolate failed attempts.</li>
</ol>

<hr/>

<h3>💾 Step 2: Save the Search</h3>
<ol>
  <li>Click <strong>Save</strong> in Discover.</li>
  <li>Name the search: <code>SSH Failed Activity</code>.</li>
</ol>

<hr/>

<h3>🚨 Step 3: Create a Brute Force Alert Rule</h3>
<ol>
  <li>Go to <strong>Alerts</strong> → <strong>Create threshold rule</strong>.</li>
  <li>Name your rule (include your handle for giveaways): <code>my-dfir-ssh-brute-force-activity-stevenrocks</code></li>
  <li>The query from Discover should be pre-filled.</li>
  <li>Set threshold: <strong>Count is above 5 in 5 minutes</strong>.</li>
  <li>Click <strong>Test query</strong> to verify hits.</li>
  <li>Set rule check frequency: every <code>1 minute</code>.</li>
  <li>Click <strong>Save rule</strong>. (Actions will be added in a later lesson.)</li>
</ol>

<hr/>

<h3>🗺️ Step 4: Build a Kibana Dashboard</h3>
<ol>
  <li>Go to <strong>Maps</strong> under <em>Analytics</em>.</li>
  <li>Paste in your KQL query from the saved search.</li>
  <li>Click <strong>Add Layer</strong> → <strong>Choropleth Layer</strong>.</li>
  <li>Use <strong>World Countries</strong> boundary and <code>source.geo.country_iso_code</code> for join field.</li>
  <li>Choose your Elasticsearch index/data view.</li>
  <li>Save the map as <strong>SSH Network Map</strong> and add to a new dashboard.</li>
  <li>Title the dashboard: <strong>SSH Authentication Activity</strong>.</li>
</ol>

<hr/>

<h3>✅ Optional: Track Successful SSH Auths</h3>
<ol>
  <li>Duplicate your saved failed query and change <code>failed</code> to <code>accepted</code>.</li>
  <li>Save it as <code>SSH Successful Authentication</code>.</li>
  <li>Display both queries side-by-side on the dashboard.</li>
</ol>

<hr/>

<h3>🎉 Recap</h3>
<ul>
  <li>🔐 Alerting is now in place for brute force SSH login attempts</li>
  <li>🗺️ Visualization layer built using Kibana Maps</li>
  <li>📈 Dashboard displays real-time insight into attack origins and frequency</li>
</ul>
