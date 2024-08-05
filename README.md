# stunnel-mimecast
Accept SMTP plaintext (unencrypted), and enforced via TLS to Mimecast smarthost

# Install stunnel on Debian or Ubuntu
````
apt update
apt install -y stunnel4
````
Download [stunnel.conf](https://github.com/mimecast-scott/stunnel-mimecast/blob/main/stunnel.conf) to /etc/stunnel/stunnel.conf, or copy and paste from below:

````
client = yes

[smtp-plaintext-to-tls13-mimecast]
accept = 0.0.0.0:25
connect = eu-smtp-outbound-1.mimecast.com:25
protocol = smtp
sslVersion = TLSv1.3
options = NO_SSLv2
options = NO_SSLv3

[smtp-tls-to-plaintext-local]
accept = 0.0.0.0:587
connect = 127.0.0.1:25
protocol = smtp
cert = /path/to/your/certificate.crt
key = /path/to/your/private.key
options = NO_SSLv2
options = NO_SSLv3
````


then run:
````
systemctl enable stunnel4
systemctl start stunnel4
````

Once done, you can test stunnel is working by telneting to `localhost:25`, you will then see the SMTP response header from Mimecast below:
````
telnet localhost:25
````

Response:
````
220 [region]-smtp-outbound-1.mimecast.com ESMTP; Sat, 27 Jul 2024 09:26:38 +0100
````
