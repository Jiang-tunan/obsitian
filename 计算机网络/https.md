1. **生成 SSL 证书**：
    
    - 使用 OpenSSL 生成私钥和自签名的 SSL 证书。
    - 将生成的证书（`.crt` 文件）和私钥（`.key` 文件）保存在安全的位置。
    - openssl genrsa -out private.key 2048
    - openssl req -new -key private.key -out certificate.csr
    - openssl x509 -req -days 365 -in certificate.csr -signkey private.key -out certificate.crt
1. **配置 Nginx 以使用 SSL**：
    
    - 在 Nginx 配置文件中的相应 `server` 块中，设置 `listen` 指令以监听 443 端口（SSL）。
    - 使用 `ssl_certificate` 和 `ssl_certificate_key` 指令指定 SSL 证书和私钥文件的路径。
    - 对于需要运行在非标准 SSL 端口的 `server` 块（如 1618），确保相应地设置了 SSL 监听指令。
    - ssl_certificate /etc/pki/ca-trust/extracted/openssl/certificate.crt;
    - ssl_certificate_key /etc/pki/tls/private/private.key;
    -         listen       1618 ssl;
	        listen       [::]:1618 ssl;
	        listen      443 ssl;
	        listen      [::]:443 ssl;
1. **检查和重载 Nginx 配置**：
    
    - 使用 `nginx -t` 命令检查配置文件的语法。
    - 使用 `systemctl reload nginx` 或类似命令重新加载 Nginx 配置。
4. **测试 HTTPS 连接**：
    
    - 尝试通过 HTTPS 协议（如 `https://192.168.31.24`）访问您的网站。
    - 如果使用自签名证书，浏览器可能会显示安全警告。
5. **防火墙和端口设置**：
    
    - 确保防火墙设置允许通过 SSL 端口（默认为 443，以及任何非标准端口，如 1618）的流量。
6. **排查和解决问题**：
    
    - 如果遇到无法访问或连接拒绝的问题，检查防火墙设置，确认 Nginx 是否正确监听指定端口。
    - 查看 Nginx 的错误日志（通常位于 `/var/log/nginx/error.log`）以获取更多信息。

## method
### GET

- **用途**：`GET`方法用于请求从指定资源获取数据。它通常用于查询或读取操作，不应当产生副作用，这意味着执行`GET`请求不会更改资源的状态。
- **数据传输**：请求的参数通常附加在URL后面，通过查询字符串传递，例如`https://example.com/api/users?id=123`。
- **幂等性**：`GET`是幂等的，意味着多次执行相同的`GET`请求应该返回相同的结果，而不会对资源产生额外影响。

### POST

- **用途**：`POST`方法用于向指定资源提交数据，通常用于创建新的资源或提交表单数据。`POST`请求可能会根据发送的数据对服务器状态进行更改或产生其他副作用。
- **数据传输**：提交的数据通常包含在请求体中，不会出现在URL中，支持多种数据格式，包括`application/x-www-form-urlencoded`、`multipart/form-data`、`application/json`等。
- **幂等性**：`POST`不是幂等的，意味着多次执行相同的`POST`请求可能会每次都产生不同的结果，例如创建多个资源。

### PUT

- **用途**：`PUT`方法用于更新现有资源或如果不存在则创建资源。与`POST`不同，`PUT`通常用于指定资源的完整更新。
- **数据传输**：与`POST`类似，`PUT`请求的数据也包含在请求体中，支持多种数据格式。`PUT`请求应提供资源的完整表示。
- **幂等性**：`PUT`是幂等的，这意味着重复执行相同的`PUT`请求应该保持资源状态不变，而不是创建或更改多个资源。换句话说，无论执行多少次，结果都应该确保资源处于同一状态。

### 总结

- **`GET`** 用于读取或查询资源，不应改变资源状态，参数通过URL传递。
- **`POST`** 用于创建新资源或提交数据，可能会改变资源状态或服务器状态，数据在请求体中。
- **`PUT`** 用于更新现有资源的全面信息或创建新资源，请求体中包含资源的更新内容，是幂等的。