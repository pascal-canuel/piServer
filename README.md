# piServer

1. Generate a CA private key

```
openssl genrsa -des3 -out CA-PrivateKey.key 2048
```

2. Generate the root certificate

```
openssl req -x509 -new -nodes -key CA-PrivateKey.key -sha256 -days 1825 -out CA-RootCert.pem
```

3. Install the root certificate. Make sure the file has the +.crt+ extension

```
sudo cp CA-RootCert.pem /usr/local/share/ca-certificates/CA-RootCert.crt
sudo update-ca-certificates
```

To remove the certificate run

```
sudo update-ca-certificates --fresh
```

4. Generate a site private key 

```
openssl genrsa -out pascalcanuel.com.key 2048
```

5. Generate a csr 

```
openssl req -new -key example.com.key -out example.com.csr
```

6. Create the +pascalcanuel.com.ext+ config file

```
 authorityKeyIdentifier=keyid,issuer
 basicConstraints=CA:FALSE
 keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
 subjectAltName = @alt_names

 [alt_names]
 DNS.1 = pascalcanuel.com
 DNS.2 = *.pascalcanuel.com
 ```

7. Generate the site certificate

```
 openssl x509 -req -in pascalcanuel.com.csr -CA CA-RootCert.pem -CAkey CA-PrivateKey.key -CAcreateserial -out pascalcanuel.com.crt -days 1825 -sha256 -extfile pascalcanuel.com.ext
 ```

