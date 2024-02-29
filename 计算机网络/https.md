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