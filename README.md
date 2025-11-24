## ✔️ **Opción C: Corregir el repositorio si ya usas 64 bits**

Primero borra el repo incorrecto:

```bash
sudo rm /etc/apt/sources.list.d/openvpn-packages.list
```

Luego instala la clave:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://packages.openvpn.net/packages-repo.gpg | sudo tee /etc/apt/keyrings/openvpn.asc
```

Ahora detecta la distro:

```bash
DISTRO=$(lsb_release -c -s)
echo "deb [signed-by=/etc/apt/keyrings/openvpn.asc] https://packages.openvpn.net/openvpn3/debian $DISTRO main" | sudo tee /etc/apt/sources.list.d/openvpn-packages.list
```

Y actualiza:

```bash
sudo apt update
```

⚠️ **Solo funcionará si tu sistema es arm64 y tu distro está soportada.**

