# STIR/SHAKEN

These are just some notes whilst we experiment. It's not the finished product.

## Generating Certificates for testing

Modified from https://blog.opensips.org/2022/10/31/how-to-generate-self-signed-stir-shaken-certificates/


`apt -y install openssl coreutils`

```
mkdir stir-shaken-ca
cd stir-shaken-ca
```

Generate a key for the CA

```
openssl ecparam -noout -name prime256v1 -genkey -out ca-key.pem
```

Generate a cert for the CA

```
openssl req -x509 -new -nodes -key ca-key.pem -sha256 -days 365 -out ca-cert.pem
```

```
cd ../
mkdir stir-shaken-sp1
cd stir-shaken-sp1
```

Generate the key for the service provider

```
openssl ecparam -noout -name prime256v1 -genkey -out sp1-key.pem
```

Prepare the certificate configuration

```
cat >TNAuthList.conf << EOF 
asn1=SEQUENCE:tn_auth_list 
[tn_auth_list] 
field1=EXP:0,IA5:1001 
EOF

openssl asn1parse -genconf TNAuthList.conf -out TNAuthList.der 

cat >openssl.conf << EOF 
[ req ] 
distinguished_name = req_distinguished_name 
req_extensions = v3_req 
[ req_distinguished_name ] 
commonName = “SHAKEN” 
[ v3_req ] 
EOF

od -An -t x1 -w TNAuthList.der | sed -e 's/ /:/g' -e 's/^/1.3.6.1.5.5.7.1.26=DER/'      >>openssl.conf
```

Create a CSR

```
openssl req -new -nodes -key sp1-key.pem -keyform PEM  -subj '/C=UK/O=DNUM/CN=SHAKEN' -sha256 -config openssl.conf -out sp1-csr.pem
```

Generate the certificate

```
openssl x509 -req -in sp1-csr.pem -CA ../stir-shaken-ca/ca-cert.pem -CAkey ../stir-shaken-ca/ca-key.pem -CAcreateserial -days 365 -sha256 -extfile openssl.conf -extensions v3_req -out sp1-cert.pem
```

## Configuring asterisk

N.B, Asterisk needs the res_stir_shaken module loaded, which might not have been built when you compiled asterisk. For reasons unknown despite having libjwt installed, asterisk didn't seem to detect it during compile time. To fix this I have to add `--with-libjwt-bundled` to the configure command.

Don't forget to fix the ownership of the certificates. Also add the ACL to acl.conf

