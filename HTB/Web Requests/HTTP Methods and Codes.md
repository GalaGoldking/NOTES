# Request Methods

<table>
  <tr>
    <th>Method</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>GET</td>
    <td>Requests a specific resource. Additional data can be passed to the server via query strings in the URL (e.g. ?param=value).</td>
  </tr>
  <tr>
    <td>POST</td>
    <td>Sends data to the server. It can handle multiple types of input, such as text, PDFs, and other forms of binary data. This data is appended in the request body present after the headers. The POST method is commonly used when sending information (e.g. forms/logins) or uploading data to a website, such as images or documents.</td>
  </tr>
  <tr>
    <td>HEAD</td>
    <td>Requests the headers that would be returned if a GET request was made to the server. It doesn't return the request body and is usually made to check the response length before downloading resources.</td>
  </tr>
  <tr>
    <td>PUT</td>
    <td>Creates new resources on the server. Allowing this method without proper controls can lead to uploading malicious resources.</td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td>Deletes an existing resource on the webserver. If not properly secured, can lead to Denial of Service (DoS) by deleting critical files on the web server.</td>
  </tr>
  <tr>
    <td>OPTIONS</td>
    <td>Returns information about the server, such as the methods accepted by it.</td>
  </tr>
  <tr>
    <td>PATCH</td>
    <td>Applies partial modifications to the resource at the specified location.</td>
  </tr>
</table>

# Response Codes

<table>
  <tr>
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>1xx</td>
    <td>Provides information and does not affect the processing of the request.</td>
  </tr>
  <tr>
    <td>2xx</td>
    <td>Returned when a request succeeds.</td>
  </tr>
  <tr>
    <td>3xx</td>
    <td>Returned when the server redirects the client.</td>
  </tr>
  <tr>
    <td>4xx</td>
    <td>Signifies improper requests from the client. For example, requesting a resource that doesn't exist or requesting a bad format.</td>
  </tr>
  <tr>
    <td>5xx</td>
    <td>Returned when there is some problem with the HTTP server itself.</td>
  </tr>
  
</table>
