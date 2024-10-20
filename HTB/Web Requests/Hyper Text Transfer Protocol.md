# URL

![image](https://github.com/user-attachments/assets/09588745-2f48-4b94-96f5-8a4b8507425e)

<table>
  <tr>
    <th>Component</th>
    <th>Example</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Scheme</td>
    <td>http:// https://</td>
    <td>This is used to identify the protocol being accessed by the client, and ends with a colon and a double slash (://)</td>
  </tr>
  <tr>
    <td>User Info</td>
    <td>admin:password@</td>
    <td>This is an optional component that contains the credentials (separated by a colon :) used to authenticate to the host, and is separated from the host with an at sign (@)</td>
  </tr>
  <tr>
    <td>Host</td>
    <td>inlanefreight.com</td>
    <td>The host signifies the resource location. This can be a hostname or an IP address</td>
  </tr>
  <tr>
    <td>Port</td>
    <td>:80</td>
    <td>The Port is separated from the Host by a colon (:). If no port is specified, http schemes default to port 80 and https default to port 443</td>
  </tr>
  <tr>
    <td>Path</td>
    <td>/dashboard.php</td>
    <td>This points to the resource being accessed, which can be a file or a folder. If there is no path specified, the server returns the default index (e.g. index.html).</td>
  </tr>
  <tr>
    <td>Query String</td>
    <td>?login=true</td>
    <td>The query string starts with a question mark (?), and consists of a parameter (e.g. login) and a value (e.g. true). Multiple parameters can be separated by an ampersand (&).</td>
  </tr>
  <tr>
    <td>Fragments</td>
    <td>#status</td>
    <td>Fragments are processed by the browsers on the client-side to locate sections within the primary resource (e.g. a header or section on the page).</td>
  </tr>
</table>
