# pomerium-ssh



sudo vi /etc/ssh/sshd_config
Port 22 -> 2222
sudo systemctl restart ssh


ssh-keygen -f ca_key
ssh-keygen -t ed25519 -f ssh_host_ed25519_key
ssh-keygen -t rsa -f ssh_host_rsa_key
ssh-keygen -t ecdsa -f ssh_host_ecdsa_key

scp ca_key.pub 192.168.10.230:
sudo mv ca_key.pub /etc/ssh/
cd /etc/ssh/
sudo chown root: ca_key.pub
sudo vi sshd_config.d/99-ca.conf
TrustedUserCAKeys /etc/ssh/ca_key.pub
sudo systemctl restart ssh

