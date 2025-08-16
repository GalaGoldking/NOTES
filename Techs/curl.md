# Base Usage
curl [URL] 

\<!DOCTYPE HTML>

\<html>\</html>

# Download page
curl [URL] -O

with specifying downloaded filename

curl [URL] -o [filename]

# Sent HEAD request

curl -I [URL]

curl -X HEAD [URL]

with headers and response

curl -i [URL]

# Full details of HTTP request and response 

curl [URL] -i

# Specify Header

curl -H '[HEADER]: [PARAMETER]' [URL]

# Specify User-Agent

curl -A 'Mozilla/5.11' [URL]

# Specify Request Method

curl -X [METHOD] [URL]

# POST data with curl

curl -X POST -d 'username=admin&password=admin' [URL]

# Using cookie with curl

curl -b '[cookie name]=[cookie parameter]' [URL]

# Saving cookie to a file

curl -c [file_to_save] [URL]
