# 🛡️ STOP4ME — UFW Firewall Manager

> **Módulo de Gestión, Auditoría y Seguridad de Cortafuegos UFW para el Ecosistema ALL4ME**

[![GitHub DanSanMar](https://img.shields.io/badge/GitHub-DanSanMar-181717?style=for-the-badge&logo=github)](https://github.com/DanSanMar)
[![Bash](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Linux](https://img.shields.io/badge/OS-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.kernel.org/)
[![Version](https://img.shields.io/badge/Version-1.7-blue?style=for-the-badge)](#)

---

## 📌 Descripción

**STOP4ME** (v1.7) es un módulo Bash interactivo y avanzado diseñado dentro del proyecto **ALL4ME** para simplificar, automatizar y auditar la gestión de cortafuegos basados en **UFW** (*Uncomplicated Firewall*) en distribuciones Linux.

Combina una interfaz en consola impulsada por **`fzf`** con un panel de estado en vivo y herramientas forenses de detección de amenazas (escaneos de puertos, ataques de fuerza bruta SSH/Auth e informes de trazabilidad por IP).

---

## ✨ Características Principales

- 🎨 **Interfaz Interactiva**: Menús con búsqueda fuzzy dinámica usando `fzf` y colores ANSI.
- 📊 **Panel de Estado en Vivo**: Cabecera animada con hora, estado de UFW, número de reglas activas, políticas por defecto (*incoming/outgoing*), nivel de *logging*, interfaz de red principal e IP local.
- ⚙️ **Multi-Distribución**: Detección e instalación automática de UFW mediante gestores de paquetes nativos (`apt`, `dnf`, `pacman`, `zypper`).
- 🧊 **Soporte de Sistemas Inmutables**: Detección de sistemas basados en **OSTree / rpm-ostree** (Fedora Silverblue, Kinoite, Bazzite, etc.) e instalación de UFW en una capa del sistema, con aplicación en vivo o preparación para el siguiente arranque.
- 🔒 **Gestión Unificada de Reglas**:
  - Permitir (**ALLOW**), Denegar (**DENY**) o Rechazar (**REJECT**).
  - Filtrado flexible por **Puerto/Servicio** (ej. `80`, `443/tcp`, `ssh`), **Dirección IP / Subred** (ej. `10.0.0.0/24`) o combinación **IP + Puerto**.
  - Inserción de reglas en una posición específica (`insert`).
  - Eliminación segura con confirmación.
- 🛡️ **Control de Estado de UFW**:
  - Consulta detallada del estado y reglas numeradas.
  - Activación (con `systemctl enable`), desactivación y recarga (*reload*).
  - Reajuste completo de fábrica (*Reset*).
- 🔍 **Auditoría Forense y Detección de Amenazas**:
  - **Detector de Escaneo de Puertos**: Identifica IPs que han impactado múltiples puertos bloqueados, con opción de bloqueo inmediato.
  - **Detector de Fuerza Bruta (SSH/Auth)**: Analiza `/var/log/auth.log` y `journalctl` en busca de intentos fallidos de inicio de sesión.
  - **Informe de Auditoría Forense por IP**: Análisis detallado de volumen de impactos, resolución DNS inversa, rango temporal, interfaces, protocolos, puertos objetivo, direcciones MAC y muestreo filtrable de trazas.
- ⚙️ **Configuración de Logging de UFW**: Selección del nivel de registro (`off`, `low`, `medium`, `high`) desde el menú.
- 📝 **Bitácora Integrada**: Registro centralizado de todas las operaciones en `/var/log/stk_mantenimiento.log`, consultable desde el propio script con filtros por `INFO`, `WARN` y `ERROR` y búsqueda con `fzf`.

---

## 📋 Requisitos del Sistema

- **Sistemas Operativos Soportados**:
  - **Debian/Ubuntu y derivados**: Debian, Ubuntu, Linux Mint, Pop!_OS, Kali, Raspbian.
  - **Red Hat/Fedora y derivados**: Fedora, RHEL, CentOS, Rocky Linux, AlmaLinux.
  - **Arch y derivados**: Arch Linux, Manjaro, EndeavourOS, Garuda.
  - **openSUSE / SUSE**.
  - **Sistemas inmutables OSTree**: Fedora Silverblue, Kinoite, Bazzite y similares.
- **Privilegios**: Ejecución como usuario root o con `sudo`.
- **Dependencias**:
  - `bash`
  - `ufw` *(se ofrece auto-instalación si no está presente)*
  - `fzf` *(requerido para los menús interactivos)*
  - `ip` de `iproute2` *(para mostrar la interfaz/IP activa en el panel)*
  - `host` *(opcional, para resolución DNS inversa en informes)*
  - `journalctl` / `systemctl` *(opcional, para logs y habilitación del servicio)*

---

## 🚀 Instalación y Uso

### 1. Clonar el repositorio
```bash
git clone https://github.com/DanSanMar/stop4me.git
cd stop4me
```

### 2. Otorgar permisos de ejecución
```bash
chmod +x stop4me.sh
```

### 3. Ejecutar el script
```bash
sudo ./stop4me.sh
```

---

## 🛠️ Estructura del Menú

```text
S T O P 4 M E  -  U F W  M A N A G E R
├── 1. ⚡ ESTADO      | Activar / Desactivar / Recargar UFW
│   ├── 📊 Ver Estado Actual y Reglas Detalladas
│   ├── 🛑 Desactivar Cortafuegos (Disable)
│   └── 🔄 Reiniciar Cortafuegos (Reload)
├── 2. 🔌 GESTIÓN     | Reglas por Puerto o Servicio o IP
│   ├── ➕ Añadir nueva regla (ALLOW / DENY / REJECT)
│   │   ├── Por Puerto / Servicio (ej: 80, 443/tcp, ssh)
│   │   ├── Por Dirección IP / Subred (ej: 10.0.0.0/24)
│   │   └── Por IP y Puerto específico
│   ├── ❌ Eliminar regla existente
│   └── 📥 Insertar regla en posición específica
├── 3. 🛡️ CONTROL     | Tráfico de Red y Auditoría de Eventos
│   ├── 1. 🛑 Tráfico Bloqueado en Tiempo Real (FZF Viewer)
│   ├── 2. 📊 Auditoría de Seguridad de Logs
│   │   ├── Detector de Escaneos de Puertos
│   │   ├── Detector de Fuerza Bruta (SSH/Auth)
│   │   └── Generador de Informe de Auditoría Forense por IP
│   ├── 3. ⚙️ Nivel de Registro de UFW (off, low, medium, high)
│   ├── 4. 📋 Bitácora Interna de Gestión (INFO / WARN / ERROR)
│   └── 5. ↩ Volver
├── 4. ⚠️ RESTART     | Restablecer Cortafuegos de Fábrica (Reset)
└── 5. ↩ Volver
```

---

## 📜 Registros y Log del Sistema

Todas las acciones administrativas realizadas desde **STOP4ME** quedan almacenadas en el archivo de auditoría del sistema:

- **Ruta de log**: `/var/log/stk_mantenimiento.log`
- **Formato**: `[YYYY-MM-DD HH:MM:SS] [NIVEL] [USUARIO] - [STOP4ME] Mensaje`
- **Permisos**: se crea automáticamente con `umask 027` y modo `640` si no existe.

---

## 👤 Autor

Desarrollado por **DanSanMar** como parte del ecosistema de herramientas de **ALL4ME**.

- **GitHub**: [@DanSanMar](https://github.com/DanSanMar)

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **GNU General Public License v3.0 (GPL-3.0)**. Consulta el archivo [`LICENSE`](LICENSE) para más detalles.
