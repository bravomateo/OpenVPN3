sudo apt update
sudo apt install apt-transport-https
sudo wget https://packages.openvpn.net/openvpn3/debian/openvpn3-repo.gpg -O /usr/share/keyrings/openvpn3-repo.gpg
echo "deb [signed-by=/usr/share/keyrings/openvpn3-repo.gpg] https://packages.openvpn.net/openvpn3/debian bookworm main" | sudo tee /etc/apt/sources.list.d/openvpn3.list
sudo apt update
sudo apt install openvpn3
