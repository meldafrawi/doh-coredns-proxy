### Encrypt your DNS requests using CoreDNS as DOH proxy

1. build
`docker build -t doh-coredns-proxy:latest .` 

2. Run
`docker run -d --name doh-coredns-proxy --restart=unless-stopped doh-coredns-proxy:latest`

3. Get container ip 
`docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' doh-coredns-proxy`

4. Use container IP as you default DNS in your network connection settings

5. Watch DNS requests logs
`docker logs -f doh-coredns-proxy`

#### Note: 

Image use Cloudflare DNS by default, if you want to use Google, or any another serice that provide DOH, change  `forward . tls://1.1.1.1 tls://1.0.0.1` line in Corefile, and build your image again.
