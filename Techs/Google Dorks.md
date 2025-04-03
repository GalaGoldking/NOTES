# Google Dorks
<ol>
  <li>Site: Finds results on a specific website or domain.</li>
  <li>Inurl: Searches for a keyword within a URL.</li>
  <li>Intitle: Finds a keyword within a webpage's title.</li>
  <li>Filetype: Locates specific file types like PDF or XLS.</li>
  <li>Link: Finds web pages linking to a specific URL.</li>
  <li>Intext: Searches for keywords within the body text of a webpage.</li>
  <li>Allintitle: Finds pages with multiple keywords in the title.</li>
  <li>Cache: Shows the cached version of a webpage.</li>
  <li>Related: Displays pages related to a specific URL.</li>
  <li>Info: Provides details about a website, including cache and similar pages.</li>
  <li>Ext: Finds a specific file extension.</li>
  <li>Define: Displays the definition of a word or phrase.</li>
  <li>Phonebook: Searches for phone numbers and contact information for a person or business.</li>
  <li>Map: Shows a map of a location or address.</li>
  <li>Allinurl: Finds pages with multiple keywords in the URL.</li>
  <li>Before: Finds content indexed before a specific date.</li>
  <li>After: Finds content indexed after a specific date.</li>
  <li>Numrange: Searches for numbers within a specified range.</li>
  <li>AROUND(X): Finds pages where two terms are within a specified number of words from each other.</li>
  <li>Inanchor: Searches for keywords within the anchor text of links on a webpage.</li>
</ol>

<table>
  <tr>
    <th>Operator</th>
    <th>Operator Description</th>
    <th>Example</th>
    <th>Example Description</th>
  </tr>
  <tr>
    <td>site:</td>
    <td>Limits the results to a specific website or domain</td>
    <td>site:example.com</td>
    <td>Find all publicly accessible pages on example.com</td>
  </tr>
  <tr>
    <td>inurl:</td>
    <td>Finds pages with a specific term in the URL.</td>
    <td>inurl:login</td>
    <td>Search for login pages on any website</td>
  </tr>
  <tr>
    <td>filetype:</td>
    <td>Searches for files of a particular type.</td>
    <td>filetype:pdf</td>
    <td>Find downloadable PDF documents.</td>
  </tr>
  <tr>
    <td>intitle:</td>
    <td>Finds pages with a specific term in the title.</td>
    <td>intitle:"confidentialreport"</td>
    <td>Look for documents titled "confidential report" or similar variations.</td>
  </tr>
  <tr>
    <td>intext: or inbody:</td>
    <td>Searches for a term within the body text of pages.</td>
    <td>intext:"password reset"</td>
    <td>Identify webpages containing the term “password reset”.</td>
  </tr>
  <tr>
    <td>cache:</td>
    <td>Displays the cached version of a webpage (if available).</td>
    <td>cache:example.com</td>
    <td>View the cached version of example.com to see its previous content.</td>
  </tr>
  <tr>
    <td>link:</td>
    <td>Finds pages that link to a specific webpage.</td>
    <td>link:example.com </td>
    <td>Identify websites linking to example.com.</td>
  </tr>
  <tr>
    <td>related:</td>
    <td>Finds websites related to a specific webpage.</td>
    <td>related:example.com</td>
    <td>Discover websites similar to example.com</td>
  </tr>
  <tr>
    <td>info:</td>
    <td>Provides a summary of information about a webpage.</td>
    <td>info:example.com</td>
    <td>Get basic details about example.com, such as its title and description.</td>
  </tr>
  <tr>
    <td>define:</td>
    <td>Provides definitions of a word or phrase.</td>
    <td>define:phishing</td>
    <td>Get a definition of "phishing" from various sources.</td>
  </tr>
  <tr>
    <td>numrange:</td>
    <td>Searches for numbers within a specific range.</td>
    <td>site:example.com numrange:1000-2000</td>
    <td>Find pages on example.com containing numbers between 1000 and 2000.</td>
  </tr>
  <tr>
    <td>allintext:</td>
    <td>Finds pages containing all specified words in the body text.</td>
    <td>allintext:admin password reset</td>
    <td>Search for pages containing both "admin" and "password reset" in the body text.</td>
  </tr>
  <tr>
    <td>allinurl:</td>
    <td>Finds pages containing all specified words in the URL</td>
    <td>allinurl:admin panel</td>
    <td>Look for pages with "admin" and "panel" in the URL.</td>
  </tr>
  <tr>
    <td>allintitle:</td>
    <td>Finds pages containing all specified words in the title.</td>
    <td>allintitle:confidential report 2023</td>
    <td>Search for pages with "confidential," "report," and "2023" in the title.</td>
  </tr>
  <tr>
    <td>AND</td>
    <td>Narrows results by requiring all terms to be present.</td>
    <td>site:example.com AND (inurl:admin OR inurl:login)</td>
    <td>Find admin or login pages specifically on example.com.</td>
  </tr>
  <tr>
    <td>OR</td>
    <td>Broadens results by including pages with any of the terms.</td>
    <td>"linux" OR "ubuntu" OR "debian"</td>
    <td>Search for webpages mentioning Linux, Ubuntu, or Debian.</td>
  </tr>
  <tr>
    <td>NOT</td>
    <td>Excludes results containing the specified term</td>
    <td>site:bank.com NOT inurl:login</td>
    <td>Find pages on bank.com excluding login pages.</td>
  </tr>
  <tr>
    <td>* (wildcard)</td>
    <td>Represents any character or word.</td>
    <td>site:socialnetwork.com filetype:pdf user* manual</td>
    <td>Search for user manuals (user guide, user handbook) in PDF format on socialnetwork.com.</td>
  </tr>
  <tr>
    <td>.. (range search)</td>
    <td>Finds results within a specified numerical range.</td>
    <td>site:ecommerce.com "price" 100..500</td>
    <td>Look for products priced between 100 and 500 on an ecommerce website.</td>
  </tr>
  <tr>
    <td>" " (quotation marks)</td>
    <td>Searches for exact phrases.</td>
    <td>"information security policy"</td>
    <td>Find documents mentioning the exact phrase "information security policy".</td>
  </tr>
  <tr>
    <td>- (minus sign)</td>
    <td>Excludes terms from the search results.</td>
    <td>site:news.com - inurl:sports</td>
    <td>Search for news articles on news.com excluding sportsrelated content.</td>
  </tr>
</table>
