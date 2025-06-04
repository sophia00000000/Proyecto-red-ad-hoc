# B.A.T.M.A.N. (Better Approach To Mobile Adhoc Networking)

Este documento describe cómo instalar y configurar **B.A.T.M.A.N.** en Ubuntu para establecer una red ad-hoc entre múltiples nodos usando el módulo `batman-adv`.

---

## 📋 Requisitos previos

Asegúrate de contar con los siguientes paquetes y privilegios de superusuario:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install build-essential git dkms linux-headers-$(uname -r)
sudo apt install batctl iw iproute2
```

Ubuntu moderno ya incluye el módulo `batman-adv`, solo necesitas cargarlo:

```bash
sudo modprobe batman-adv
```

Para que se cargue automáticamente en cada arranque:

```bash
echo batman-adv | sudo tee -a /etc/modules
```

---

## ⚙️ Configuración de la interfaz de red

Desconectar `wlp0s20f3` de NetworkManager:

```bash
sudo nmcli device set wlp0s20f3 managed no
```

Establecer el modo ad-hoc y levantar la interfaz:

```bash
sudo ip link set wlp0s20f3 down
sudo iwconfig wlp0s20f3 mode ad-hoc
sudo ip link set wlp0s20f3 up
```

Unirse a la red ad-hoc:

```bash
sudo iwconfig wlp0s20f3 mode ad-hoc
sudo iwconfig wlp0s20f3 essid red-angie
sudo iwconfig wlp0s20f3 channel 1
sudo ip link set wlp0s20f3 up
```

Verificar conexión (debe mostrar una "Cell" con dirección MAC):

```bash
iwconfig
```

---

## 🛰 Activar BATMAN-adv sobre la interfaz Wi-Fi

```bash
sudo modprobe batman-adv
sudo batctl if add wlp0s20f3
sudo ip link set up dev bat0
```

Verificar que la interfaz está activa:

```bash
sudo batctl if
```

Debe aparecer como:

```
wlp0s20f3: active
```

---

## 🌐 Asignar IP a `bat0`

En **cada nodo**, asigna una IP diferente dentro del rango `10.0.0.0/24`:

```bash
sudo ip addr add 10.0.0.X/24 dev bat0
```

Reemplaza `X` con el número de nodo, por ejemplo: `10.0.0.1`, `10.0.0.2`, etc.

---

## ✅ Comprobación

Puedes usar `ping` entre nodos para verificar la conectividad:

```bash
ping 10.0.0.2
```

---

## 📚 Más información

- [Documentación oficial](https://www.open-mesh.org/projects/batman-adv/wiki)
- [batctl Manual](https://manpages.debian.org/testing/batctl/batctl.8.en.html)
