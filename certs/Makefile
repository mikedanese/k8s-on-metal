SHELL := /bin/bash

all: ca.pem apiserver.pem node.pem

clean:
	rm -f *.pem *.srl

# private keys
ca-key.pem apiserver-key.pem node-key.pem:
	openssl genrsa -out $@ 2048

# self signed CA public key
ca.pem: ca-key.pem
	openssl req -x509 -new -nodes -key ca-key.pem -days 10000 -out ca.pem -subj "/CN=kube-ca"

apiserver.pem: ca.pem ca-key.pem openssl.cnf apiserver-key.pem
	openssl x509 -req -CA ca.pem -CAkey ca-key.pem -out apiserver.pem -days 365 -extensions v3_req -extfile openssl.cnf -CAcreateserial \
		-in <(openssl req -new -key apiserver-key.pem -subj "/CN=kube-apiserver" -config openssl.cnf)

node.pem: ca.pem ca-key.pem node-key.pem
	openssl x509 -req -CA ca.pem -CAkey ca-key.pem -out node.pem -days 365 -CAcreateserial \
		-in <(openssl req -new -key node-key.pem -subj "/CN=node")
