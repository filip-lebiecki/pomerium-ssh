# pomerium-ssh

PROXY:

1) Change SSH port to 2222/TCP

```
sudo vi /etc/ssh/sshd_config
Port 22 -> 2222
sudo systemctl restart ssh
```

2) Generate SSH keys

```
ssh-keygen -f ca_key
ssh-keygen -t ed25519 -f ssh_host_ed25519_key
ssh-keygen -t rsa -f ssh_host_rsa_key
ssh-keygen -t ecdsa -f ssh_host_ecdsa_key
```

3) Copy CA key to target SSH server(s):

```
scp ca_key.pub 192.168.10.230:
```

TARGET SSH SERVER (NODE1):

4) Trust CA public key on target server
   
```
sudo mv ca_key.pub /etc/ssh/
cd /etc/ssh/
sudo chown root: ca_key.pub
sudo vi sshd_config.d/99-ca.conf
TrustedUserCAKeys /etc/ssh/ca_key.pub
sudo systemctl restart ssh
```

CLIENT:

5) Create Google OAuth2 credentials
6) Create Native App on Auth0 with Device Code enabled
   
PROXY:

7) Put Auth0 credentials in Pomerium Proxy config and start the proxy

```
vi config.yaml
```

Update values

```
idp_provider_url: https://AUTH0-DOMAIN-HERE
idp_client_id: AUTH0 CLIENT ID HERE
idp_client_secret: AUTH0 CLIENT SECRET HERE
docker compose up -d
docker ps
```
