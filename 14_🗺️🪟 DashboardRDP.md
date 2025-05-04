<h1>Authentication Visualization: Maps & Dashboards (RDP + SSH)</h1>

<nav>
  <h3>📚 Table of Contents</h3>
  <ul>
    <li><a href="#demo">Demo: Start with Maps</a></li>
    <li><a href="#map-failed">Create Map for Failed Authentications</a></li>
    <li><a href="#map-success">Create Map for Successful Authentications</a></li>
    <li><a href="#tables">Build Visualization Tables</a></li>
    <li><a href="#dashboard">Improve Dashboard Layout</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
  </ul>
</nav>

<h2 id="demo">🖥️ Demo: Start with Maps</h2>
<ul>
  <li>Open <strong>Elastic GUI → Maps</strong> via the ☰ hamburger menu</li>
  <li>Recall your saved search for failed RDP login events</li>
  <li>Query example:
    <pre><code>event.code:4625 AND agent.name:mydfir-win-stephenrocks</code></pre>
  </li>
</ul>

<h2 id="map-failed">🔎 Create Map for Failed Authentications</h2>
<ol>
  <li>In Maps, click <strong>Add Layer → Choropleth map</strong></li>
  <li>Use <strong>World Countries</strong> for the boundary layer</li>
  <li>Join field:
    <pre><code>source.geo.country_iso_code</code></pre>
  </li>
  <li>Observe high activity: e.g., 39,000+ failed RDP attempts from Russia</li>
  <li>Save map as: <strong>RDP Failed Authentication</strong></li>
  <li>Attach it to dashboard: <code>mydfir-authentication-activity</code></li>
</ol>

<h2 id="map-success">🚀 Create Map for Successful Authentications</h2>
<ol>
  <li>Switch to query:
    <pre><code>event.code:4624</code></pre>
  </li>
  <li>Filter by logon types:
    <pre><code>winlog.event_data.LogonType: 10 OR 7</code></pre>
  </li>
  <li>Save search as: <code>RDP Successful Activity</code></li>
  <li>Duplicate previous map layer and update the query to reflect success events</li>
  <li>Save updated map as: <strong>RDP Successful Authentications</strong></li>
</ol>

<h2 id="tables">📈 Build Visualization Tables</h2>
<ol>
  <li>Go to <strong>Visualizations</strong> → <strong>Create Table</strong></li>
  <li>Add fields:
    <ul>
      <li>user.name</li>
      <li>source.ip</li>
      <li>source.geo.country_name</li>
    </ul>
  </li>
  <li>Adjust table settings:
    <ul>
      <li>Sort by count descending</li>
      <li>Set top values from 3 to 10</li>
      <li>Uncheck “Group remaining values as Other”</li>
    </ul>
  </li>
  <li>Save four visualizations:
    <ul>
      <li><code>SSH Failed Authentications (Table)</code></li>
      <li><code>SSH Successful Authentications (Table)</code></li>
      <li><code>RDP Failed Authentications (Table)</code></li>
      <li><code>RDP Successful Authentications (Table)</code></li>
    </ul>
  </li>
</ol>

<h2 id="dashboard">🧩 Improve Dashboard Layout</h2>
<ul>
  <li>Place both map layers and table visualizations into one unified dashboard</li>
  <li>Label and align sections for:
    <ul>
      <li>Failed vs. Successful</li>
      <li>RDP vs. SSH</li>
    </ul>
  </li>
  <li>Adjust dashboard time filters (e.g., Last 15 minutes, Last 7 days)</li>
</ul>

<h2 id="conclusion">🧠 Conclusion</h2>
<ul>
  <li>Visualized both failed and successful RDP and SSH login activity</li>
  <li>Built maps and tables for better investigation and threat intel</li>
  <li>Encouraged to create more advanced visualizations using filters, heatmaps, and timelines</li>
</ul>
