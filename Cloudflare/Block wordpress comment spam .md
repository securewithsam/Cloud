#### Form and Comment Spam (Expression)
![image](https://github.com/securewithsam/Cloud/assets/85324643/1243b40c-8012-4be8-9ab0-5cf419acb0c8)

```sh
(http.request.uri contains "/wp-admin/admin-ajax.php" and http.request.method eq "POST" and not http.referer contains "yourwebsitehere.com") or (http.request.uri contains "/wp-comments-post.php" and http.request.method eq "POST" and not http.referer contains "yourwebsitehere.com")
```
####  Challenge Comment Spam 
![image](https://github.com/securewithsam/Cloud/assets/85324643/0936782a-9a9d-4f53-b5ea-2beee38c7ee6)

```sh
(http.request.uri.path contains "comments-post.php") or (http.request.uri.path contains "/?replytocom=")
```
 Or

![image](https://github.com/securewithsam/Cloud/assets/85324643/0abad31f-b007-497c-b59d-e5b01da90ddd)



