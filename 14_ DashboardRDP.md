<h2>🖥️ Demo</h2>
<ul>
  <li>Access Elastic Web GUI and navigate to <strong>Maps</strong> via the hamburger menu.</li>
  <li>Recall the saved Discover search query for failed RDP authentications.</li>
  <li>Query used: <code>event.code:4625 AND agent.name:mydfir-win-stephenrocks</code>.</li>
</ul>

<h2>🔎 Creating Map for Failed Authentications</h2>
<ul>
  <li>In Maps, add a new layer: select <strong>choropleth map</strong>.</li>
  <li>Use <strong>World Countries</strong> as the boundary.</li>
  <li>Join field: <code>source.geo.country_iso_code</code>.</li>
  <li>Result: 39,000+ failed RDP attempts from Russia.</li>
  <li>Save the map under the title: <strong>RDP Failed Authentication</strong>.</li>
  <li>Link to existing dashboard: <strong>mydfir-authentication-activity</strong>.</li>
</ul>

<h2>🚀 Creating Map for Successful Authentications</h2>
<ul>
  <li>Switch Discover query to <code>event.code:4624</code> (successful authentications).</li>
  <li>Identify successful RDP login attempts using logon types 10 and 7.</li>
  <li>Field: <code>winlog.event_data.LogonType</code> (10 or 7).</li>
  <li>Save search as: <strong>RDP Successful Activity</strong>.</li>
  <li>Duplicate map layer, adjust query, and save as <strong>RDP Successful Authentications</strong>.</li>
</ul>

<h2>📈 Building Visualization Tables</h2>
<ul>
  <li>Create tables in Visualizations instead of bar charts.</li>
  <li>Fields to add: Username, Source IP, Country.</li>
  <li>Steps:</li>
  <ul>
    <li>Sort counts descending.</li>
    <li>Adjust 'Top Values' from 3 to 10.</li>
    <li>Uncheck "Group remaining values as Other" under Advanced settings.</li>
  </ul>
  <li>Save visualizations as:</li>
  <ul>
    <li><strong>SSH Failed Authentications (Table)</strong></li>
    <li><strong>SSH Successful Authentications (Table)</strong></li>
    <li><strong>RDP Failed Authentications (Table)</strong></li>
    <li><strong>RDP Successful Authentications (Table)</strong></li>
  </ul>
</ul>

<h2>🧩 Improving the Dashboard</h2>
<ul>
  <li>Align maps and tables together for better at-a-glance review.</li>
  <li>Display usernames, IPs, and country names for both failed and successful SSH and RDP authentications.</li>
  <li>Adjust dashboard time frames for recent activity (15 minutes, 7 days, etc.).</li>
</ul>

<h2>🧠 Conclusion</h2>
<ul>
  <li>Now have two maps and two tables for both RDP and SSH activities (failed and successful).</li>
  <li>Encouraged to create additional visualizations and dashboards for practice.</li>
</ul>


