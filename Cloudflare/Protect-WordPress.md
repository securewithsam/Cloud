
#### WAF

```sh
(http.request.uri.path contains "/wp-admin") or (http.request.uri.path contains "/wp-login") or (http.request.uri.path contains "/xmlrpc.php") or (http.request.uri.path contains "admin-ajax.php")
```

#### Rate Limiting
```sh
(http.request.uri.path contains "/wp-login.php") or (http.request.uri.path contains "/wp-admin/") or (http.request.uri.path contains "/wp-json/wp/v2/users") or (http.request.uri.path contains "/wp-json/wp/v2/comments") or (http.request.uri.path contains "/xmlrpc.php") or (http.request.uri.path contains "/wp-content/plugins/") or (http.request.uri.path contains "/wp-includes/") or (http.request.uri.path contains "/wp-content/themes/") or (http.request.uri.path contains "/wp-json/wp/v2/*") or (http.request.uri.path contains "/wp-content/*")
```
