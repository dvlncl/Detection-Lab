<div style="font-family: Arial, sans-serif; line-height: 1.6; font-size: 16px;">
  <h2>🔍 Elastic Stack Overview</h2>
  
  <p><strong>📦 🇪 Elasticsearch</strong> = <em>Database (Search & Indexing Engine)</em><br>
  <span style="color: gray;">How to Query:</span> <strong>ES|QL</strong>, <strong>REST API</strong></p>

  <p><strong>🔬 🇱 Logstash</strong> = <em>Data Processing Pipeline</em><br>
  <span style="color: gray;">Purpose:</span> Collect, parse, and enrich telemetry data.</p>

  <p style="margin-left: 20px;"><strong>Popular Telemetry Collectors:</strong></p>
  <ul style="margin-left: 40px;">
    <li><strong>Beats</strong> (Lightweight agents)</li>
    <ul>
      <li><strong>Filebeat</strong> – Collects log files</li>
      <li><strong>Metricbeat</strong> – Collects system metrics</li>
      <li><strong>Winlogbeat</strong> – Windows event logs</li>
      <li><strong>Auditbeat</strong> – Audit framework data</li>
      <li><strong>Heartbeat</strong> – Monitors uptime</li>
    </ul>
    <li><strong>Elastic Agent</strong> – Unified telemetry shipper for logs, metrics, and security data</li>
  </ul>

  <p><strong>🥷🏽 🇰 Kibana</strong> = <em>Web Console & Visualization UI</em><br>
  <span style="color: gray;">Tool:</span> <strong>Lens</strong> for easy drag-and-drop dashboards.</p>
</div>

<table border="1" cellpadding="6" cellspacing="0">
  <thead>
    <tr>
      <th>SIEM Component Role</th>
      <th>🦨 Splunk</th>
      <th>🦆 Elastic Stack</th>
      <th>🙌🏼 Sumo Logic</th>
      <th>🦉 Arkime</th>
      <th>🐶 Graylog</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Indexer / Search Engine</strong></td>
      <td>Indexer / Search Head</td>
      <td>Elasticsearch</td>
      <td>Cloud-native index & search</td>
      <td>Elasticsearch</td>
      <td>Elasticsearch</td>
    </tr>
    <tr>
      <td><strong>Data Collector</strong></td>
      <td>Universal / Heavy Forwarder</td>
      <td>Logstash / Beats</td>
      <td>Installed / Hosted Collectors</td>
      <td>Capture Nodes</td>
      <td>Sidecar + Collectors</td>
    </tr>
    <tr>
      <td><strong>Web UI / Visualization</strong></td>
      <td>Splunk Web</td>
      <td>Kibana</td>
      <td>Sumo Logic Web UI</td>
      <td>Arkime Web UI</td>
      <td>Graylog Web Interface</td>
    </tr>
    <tr>
      <td><strong>Parsing & Enrichment</strong></td>
      <td>Heavy Forwarder, props.conf</td>
      <td>Logstash / Pipelines</td>
      <td>Cloud field extraction</td>
      <td>Packet Metadata / Tags</td>
      <td>Pipelines / Extractors</td>
    </tr>
    <tr>
      <td><strong>Alerting / Detection</strong></td>
      <td>Correlation Searches</td>
      <td>Kibana Alerts / Watcher</td>
      <td>Scheduled Searches</td>
      <td>Tag-based Scripting</td>
      <td>Streams & Alerts</td>
    </tr>
    <tr>
      <td><strong>Dashboards</strong></td>
      <td>Splunk Dashboards</td>
      <td>Kibana Visualizations</td>
      <td>Custom / Prebuilt Dashboards</td>
      <td>Session Views</td>
      <td>Custom Dashboards</td>
    </tr>
    <tr>
      <td><strong>Deployment Model</strong></td>
      <td>On-prem / Cloud / Hybrid</td>
      <td>On-prem / Cloud / Hybrid</td>
      <td>Fully Cloud (SaaS)</td>
      <td>On-prem Only</td>
      <td>On-prem / Hybrid</td>
    </tr>
    <tr>
      <td><strong>Use Case Focus</strong></td>
      <td>General SIEM / SOC</td>
      <td>Flexible + Add-ons</td>
      <td>Cloud Monitoring / DevOps</td>
      <td>Network Forensics</td>
      <td>Lightweight Log SIEM</td>
    </tr>
  </tbody>
</table>
