# 🕹️ Minecraft en Modo Offline Multijugador (Linux)

Este instructivo documenta cómo configurar un entorno de Minecraft multijugador en **modo offline**, usando:

- 🌐 [itzg/docker-minecraft-server](https://github.com/itzg/docker-minecraft-server) para el servidor en Docker
- 🖥️ [Prism Launcher](https://github.com/PrismLauncher/PrismLauncher) para lanzar el cliente
- 🔧 Opcional: bypass de cuenta Microsoft para jugar offline

---

## 🧱 Paso 1: Levantar el servidor en Docker

Ejecutá el siguiente comando para iniciar el servidor de Minecraft en modo offline:

```bash
docker run -d \
  -e EULA=TRUE \
  -e ONLINE_MODE=FALSE \
  -p 25565:25565 \
  --name minecraft \
  -v ~/minecraft-data:/data \
  itzg/minecraft-server
```

- `EULA=TRUE`: Aceptás los términos de uso de Mojang.
- `ONLINE_MODE=FALSE`: Permite jugadores en modo offline (sin cuenta Microsoft).
- `~/minecraft-data`: Se guarda el mundo y la configuración persistente.
- `-p 25565:25565`: Expone el puerto clásico de Minecraft.

---

## 💻 Paso 2: Instalar y configurar Prism Launcher (cliente offline)

### Descargar y ejecutar la AppImage:

```bash
curl -LO https://github.com/PrismLauncher/PrismLauncher/releases/download/9.4/PrismLauncher-Linux-x86_64.AppImage
chmod +x ./PrismLauncher-Linux-x86_64.AppImage
./PrismLauncher-Linux-x86_64.AppImage
```

### Bypass para permitir cuentas offline (si se requiere login Microsoft):

```bash
echo '{"accounts": [{"entitlement": {"canPlayMinecraft": true,"ownsMinecraft": true},"type": "MSA"}],"formatVersion": 3}' > ~/.local/share/PrismLauncher/accounts.json
```

Luego reiniciá Prism Launcher.

---

## 🎮 Paso 3: Crear una instancia en Prism Launcher

1. Clic en "Agregar Instancia".
2. Elegí una versión de Minecraft (por ejemplo, `1.20.1`).
3. Crear cuenta offline:
   - Ir a **"Cuentas" > "Gestionar cuentas"**
   - Clic en "Agregar cuenta offline"
   - Ingresar un nombre de usuario (por ejemplo: `jugador01`)
4. Iniciar la instancia.

---

## 🔗 Paso 4: Conectarse al servidor Docker

1. En el cliente, elegí "Multijugador".
2. Agregá el servidor:
   - Dirección IP: `192.168.x.x:25565` (según la IP de tu máquina con Docker)
3. Entrá y ¡jugá!

---

## 📦 Repositorios utilizados

- [itzg/docker-minecraft-server](https://github.com/itzg/docker-minecraft-server)
- [PrismLauncher/PrismLauncher](https://github.com/PrismLauncher/PrismLauncher)
- [antunnitraj/Prism-Launcher-PolyMC-Offline-Bypass](https://github.com/antunnitraj/Prism-Launcher-PolyMC-Offline-Bypass)

---

## 🛡️ Consideraciones

- Este setup está pensado para uso doméstico, educativo o privado.
- No permite conectarse a servidores oficiales.
- Asegurate que tu red permite conexiones entre cliente y servidor.
