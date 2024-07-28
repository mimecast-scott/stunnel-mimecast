# stunnel-mimecast
Accept SMTP plaintext (unencrypted), and enforced via TLS to Mimecast smarthost

# Install stunnel on Debian or Ubuntu
````
apt update
apt install -y stunnel4
````
Download stunnel.conf to /etc/stunnel/stunnel.conf

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
