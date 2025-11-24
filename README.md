

# ✅ **CÓMO INSTALAR OPENVPN3 CORRECTAMENTE EN RASPBERRY PI OS 64-bit**

### 1️⃣ Verifica tu arquitectura:

Debe ser **aarch64** (arm64):

```bash
uname -m
```

Debe mostrar:

```
aarch64
```

---

### 2️⃣ Crea el keyring:

```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://packages.openvpn.net/packages-repo.gpg | sudo tee /etc/apt/keyrings/openvpn.asc
```

---

### 3️⃣ Detecta tu distribución **correctamente**

No uses solo `lsb_release -cs` porque Raspberry Pi OS “bookworm” a veces devuelve valores que OpenVPN NO soporta directamente.

Ejecuta:

```bash
DISTRO=$(awk -F= '/^VERSION_CODENAME/{print $2}' /etc/os-release)
echo $DISTRO
```

Debe salir:

```
bookworm
```

---

### 4️⃣ Agrega el repositorio PERO SOLO PARA ARM64:

```bash
echo "deb [arch=arm64 signed-by=/etc/apt/keyrings/openvpn.asc] https://packages.openvpn.net/openvpn3/debian $DISTRO main" | \
sudo tee /etc/apt/sources.list.d/openvpn3.list
```

---

### 5️⃣ Actualiza:

```bash
sudo apt update
```

⚠️ **Si aún ves errores de armhf**, debes deshabilitar armhf temporalmente:

```bash
echo "APT::Architectures { \"arm64\"; };" | sudo tee /etc/apt/apt.conf.d/99arm64
sudo apt update
```

---

### 6️⃣ Instala:

```bash
sudo apt install openvpn3
```

---

# 📌 **Si quieres, puedo revisar tu `/etc/os-release` para confirmar qué repositorio debes usar**

Solo ejecuta:

```bash
cat /etc/os-release
```

y envíame el resultado.

---

# 📌 **Si deseas eliminar por completo el repositorio de nuevo**, usa:

```bash
sudo rm /etc/apt/sources.list.d/openvpn3.list
sudo rm /etc/apt/keyrings/openvpn.asc
sudo rm /etc/apt/apt.conf.d/99arm64
sudo apt update
```

---

Si quieres, también puedo darte un **script completo** para automatizar toda la instalación de forma limpia.
