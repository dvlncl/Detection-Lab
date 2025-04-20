<h2>🛡️ Sysmon Event IDs – Real-World Monitoring Reference</h2>

<p>Below is a comprehensive list of Sysmon Event IDs, their descriptions, and typical use cases in security monitoring and threat detection.</p>

<table border="1" cellpadding="5" cellspacing="0">
  <thead>
    <tr>
      <th>Event ID</th>
      <th>Description</th>
      <th>Use Case</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>1</strong></td>
      <td>Process Creation</td>
      <td>Logs details of newly created processes, including command line, hashes, and parent process information. Useful for detecting suspicious process executions.</td>
    </tr>
    <tr>
      <td><strong>2</strong></td>
      <td>File Creation Time Changed</td>
      <td>Indicates when a process changes the creation time of a file. Can help detect timestomping attempts by malware.</td>
    </tr>
    <tr>
      <td><strong>3</strong></td>
      <td>Network Connection</td>
      <td>Logs TCP/UDP connections initiated by processes, including source and destination IPs and ports. Disabled by default; useful for detecting unauthorized network activity.</td>
    </tr>
    <tr>
      <td><strong>4</strong></td>
      <td>Sysmon Service State Changed</td>
      <td>Reports when the Sysmon service starts or stops. Can indicate tampering if unexpected.</td>
    </tr>
    <tr>
      <td><strong>5</strong></td>
      <td>Process Terminated</td>
      <td>Logs when a process terminates. Useful for tracking process lifecycles and detecting abrupt terminations.</td>
    </tr>
    <tr>
      <td><strong>6</strong></td>
      <td>Driver Loaded</td>
      <td>Captures information about drivers loaded into the system, including hashes and signatures. Helps detect unauthorized or malicious drivers.</td>
    </tr>
    <tr>
      <td><strong>7</strong></td>
      <td>Image Loaded</td>
      <td>Logs when modules (e.g., DLLs) are loaded into processes. Disabled by default; useful for detecting DLL injection or hijacking.</td>
    </tr>
    <tr>
      <td><strong>8</strong></td>
      <td>CreateRemoteThread</td>
      <td>Detects when a process creates a thread in another process, a technique often used in code injection attacks.</td>
    </tr>
    <tr>
      <td><strong>9</strong></td>
      <td>RawAccessRead</td>
      <td>Indicates when a process reads data from the disk using raw access. May signify attempts to bypass file system APIs.</td>
    </tr>
    <tr>
      <td><strong>10</strong></td>
      <td>Process Access</td>
      <td>Logs when a process opens another process, which can be used to detect credential dumping or process injection attempts.</td>
    </tr>
    <tr>
      <td><strong>11</strong></td>
      <td>File Created</td>
      <td>Captures file creation events, including file name and path. Useful for monitoring file system changes.</td>
    </tr>
    <tr>
      <td><strong>12</strong></td>
      <td>Registry Object Added or Deleted</td>
      <td>Logs creation and deletion of registry keys and values. Helps detect persistence mechanisms.</td>
    </tr>
    <tr>
      <td><strong>13</strong></td>
      <td>Registry Value Set</td>
      <td>Indicates when a registry value is modified. Useful for tracking configuration changes.</td>
    </tr>
    <tr>
      <td><strong>14</strong></td>
      <td>Registry Object Renamed</td>
      <td>Logs renaming of registry keys or values. Can signal attempts to obfuscate malicious entries.</td>
    </tr>
    <tr>
      <td><strong>15</strong></td>
      <td>File Create Stream Hash</td>
      <td>Captures creation of alternate data streams, often used to hide data or code.</td>
    </tr>
    <tr>
      <td><strong>16</strong></td>
      <td>Sysmon Configuration Change</td>
      <td>Logs changes to the Sysmon configuration. Important for detecting unauthorized modifications.</td>
    </tr>
    <tr>
      <td><strong>17</strong></td>
      <td>Pipe Created</td>
      <td>Indicates when a named pipe is created. Useful for detecting inter-process communication channels used by malware.</td>
    </tr>
    <tr>
      <td><strong>18</strong></td>
      <td>Pipe Connected</td>
      <td>Logs when a process connects to a named pipe. Helps monitor IPC mechanisms.</td>
    </tr>
    <tr>
      <td><strong>19</strong></td>
      <td>WMI Event Filter</td>
      <td>Captures registration of WMI event filters, which can be used for persistence.</td>
    </tr>
    <tr>
      <td><strong>20</strong></td>
      <td>WMI Event Consumer</td>
      <td>Logs registration of WMI event consumers. Monitoring this helps detect WMI-based attacks.</td>
    </tr>
    <tr>
      <td><strong>21</strong></td>
      <td>WMI Event Consumer To Filter</td>
      <td>Indicates binding between WMI event filters and consumers. Important for tracking WMI persistence mechanisms.</td>
    </tr>
    <tr>
      <td><strong>22</strong></td>
      <td>DNS Query</td>
      <td>Logs DNS queries made by processes, including query results. Useful for detecting domain generation algorithm (DGA) activity.</td>
    </tr>
    <tr>
      <td><strong>23</strong></td>
      <td>File Delete</td>
      <td>Captures file deletion events. Helps in identifying attempts to cover tracks.</td>
    </tr>
    <tr>
      <td><strong>24</strong></td>
      <td>Clipboard Change</td>
      <td>Monitors changes to the clipboard. Can detect data exfiltration attempts via clipboard.</td>
    </tr>
    <tr>
      <td><strong>25</strong></td>
      <td>Process Tampering</td>
      <td>Detects attempts to tam
::contentReference[oaicite:0]{index=0}
 
