# Curl - useful examples

`-s, --silent` - Silent or quiet mode. Don't show progress meter (when downloading) or error messages.

`-X, --request <command>` - Specifies a  custom request method to use when communicating with the HTTP server.

` -L, --location` - follows a redirect

`-S, --show-error` - When used with -s, --silent, it makes curl show an error message if it fails.

`-f, --fail` - Fail silently (no output at all) on server errors.

`-o, --output <file>` - Write output to <file> instead of stdout.

`I, --head` - Fetch the headers only!

`-u, --user <user:password>` - Specify the user name and password to use for server authentication

## Examples 

Download content of a file and write it to output file `test.out`

```
curl  http://www.google.com/imghp -o test.out
```

```
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  4414    0  4414    0     0  88280      0 --:--:-- --:--:-- --:--:-- 88280
```
---

Download content of a file and write it to output file `test.out` but without showing progress meter

```
curl -s http://www.google.com/imghp -o test.out
```

```
```
---
Fetch the headers only without downloading resource content.
```
curl -I http://www.google.com/imghpx
```

```
HTTP/1.1 404 Not Found
Content-Type: text/html; charset=UTF-8
Referrer-Policy: no-referrer
Content-Length: 1567
Date: Sat, 27 Jun 2020 21:46:17 GMT

```
---

When requesting a non existing resource, fail and return non zero exit code.

```
curl -s -f http://www.google.com/notexisting -o test.dat || echo "failure"
```
```
failure
```

---
Try to download not existing resource, hide progress but show server error code and fail with non zero exit code 

```
curl -S -s -f http://www.google.com/notexisting -o test.dat 2>&1
```

```
curl: (22) The requested URL returned error: 404 Not Found
```

---

Make a request with credentials for resource requiring server authentication

```
curl -u username:password http://example.tld/
```