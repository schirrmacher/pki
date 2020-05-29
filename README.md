# How to Create a PKI

## List Algorithms

```
openssl ecparam -list_curves
```

## Create CA Keys

```
openssl ecparam -out ca-priv-key.pem -name prime256v1 -genkey

openssl req -new -key ca-priv-key.pem -x509 -nodes -days 365 -out ca-cert.pem -config ca.cnf
```

## Create Server Keys

```
openssl ecparam -out server-priv-key.pem -name c2pnb163v1 -genkey
```

## Make a Server Signing Request

```
openssl req -new -config server.cnf -key server-priv-key.pem -out server-sign-req.pem
```

## Create a Signature

```
openssl x509 -req -extfile server.cnf -days 999 -passin "pass:password" -in server-sign-req.pem -CA ca-cert.pem -CAkey ca-priv-key.pem -CAcreateserial -out server-cert.pem
```
