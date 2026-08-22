# 🛡️ STOP4ME — UFW Firewall Manager

> **Módulo de Gestión, Auditoría y Seguridad de Cortafuegos UFW para el Ecosistema ALL4ME**

[![GitHub DanSanMar](https://img.shields.io/badge/GitHub-DanSanMar-181717?style=for-the-badge&logo=github)](https://github.com/DanSanMar)
[![Bash](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![Linux](https://img.shields.io/badge/OS-Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)](https://www.kernel.org/)
[![Version](https://img.shields.io/badge/Version-1.5-blue?style=for-the-badge)](#)

---

## 📌 Descripción

**STOP4ME** (v1.5) es un módulo Bash interactivo y avanzado diseñado dentro del proyecto **ALL4ME** para simplificar, automatizar y auditar la gestión de cortafuegos basados en **UFW** (*Uncomplicated Firewall*) en distribuciones Linux. 

Combina una interfaz en consola impulsada por **`fzf`** con herramientas forenses de detección de amenazas (escaneos de puertos, ataques de fuerza bruta SSH/Auth e informes de trazabilidad IP).

---

## ✨ Características Principales

- 🎨 **Interfaz Interactiva**: Menús con búsqueda fuzzy dinámica usando `fzf` y colores ANSI.
- ⚙️ **Multi-Distribución**: Detección e instalación automática de UFW mediante gestores de paquetes nativos (`apt`, `dnf`, `pacman`, `zypper`).
- 🔒 **Gestión Unificada de Reglas**:
  - Permitir (**ALLOW**), Denegar (**DENY**) o Rechazar (**REJECT**).
  - Filtrado flexible por **Puerto/Servicio** (ej. `80`, `443/tcp`, `ssh`), **Dirección IP / Subred** (ej. `10.0.0.0/24`) o combinación **IP + Puerto**.
  - Reordenamiento e inserción directa de reglas por posición (`insert`).
  - Eliminación segura con confirmación.
- 🔍 **Auditoría Forense y Detección de Amenazas**:
  - **Detector de Escaneo de Puertos**: Identifica IPs que han impactado múltiples puertos bloqueados.
  - **Detector de Fuerza Bruta (SSH/Auth)**: Analiza `/var/log/auth.log` y `journalctl` en busca de intentos fallidos de inicio de sesión.
  - **Informe de Auditoría Forense por IP**: Análisis detallado de volumen de impactos, resolución DNS inversa, rango temporal, interfaces, protocolos, puertos objetivo y direcciones MAC.
- ⚡ **Control de Estado de UFW**: Verificación, activación, desactivación, recarga y reajuste completo de fábrica (*Reset*).
- 📝 **Bitácora Integrada**: Registro centralizado de todas las operaciones realizadas en `/var/log/stk_mantenimiento.log`.

---

## 📋 Requisitos del Sistema

- **Sistemas Operativos Soportados**: Debian, Ubuntu, Linux Mint, Pop!_OS, Kali, Raspbian, Fedora, RHEL, CentOS, Rocky Linux, AlmaLinux, Arch Linux, Manjaro, openSUSE.
- **Privilegios**: Ejecución como usuario root o con `sudo`.
- **Dependencias**:
  - `bash`
  - `ufw` *(se ofrece auto-instalación si no está presente)*
  - `fzf` *(requerido para los menús interactivos)*
  - `host` *(opcional, para resolución DNS en informes)*

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
├── 1. ⚡ Estado / Activar / Desactivar / Recargar UFW
├── 2. 🔌 Gestión de Reglas por Puerto o Servicio o IP (ALLOW/DENY/REJECT)
│   ├── ➕ Añadir nueva regla (Puerto / IP / Combinado)
│   ├── ❌ Eliminar regla existente
│   └── 📥 Insertar regla en posición específica
├── 3. 🛡️ Control de Tráfico de Red y Auditoría de Eventos
│   ├── 1. 🛑 Tráfico Bloqueado en Tiempo Real (FZF Viewer)
│   ├── 2. 📊 Auditoría de Seguridad
│   │   ├── Detector de Escaneos de Puertos
│   │   ├── Detector de Fuerza Bruta (SSH)
│   │   └── Generador de Informe de Auditoría Forense por IP
│   ├── 3. ⚙️ Nivel de Registro de UFW (off, low, medium, high)
│   └── 4. 📋 Bitácora Interna de Gestión
└── 4. ⚠️ Restablecer Cortafuegos de Fábrica (Reset)
```

---

## 📜 Registros y Log del Sistema

Todas las acciones administrativas realizadas desde **STOP4ME** quedan almacenadas en el archivo de auditoría del sistema:

- **Ruta de log**: `/var/log/stk_mantenimiento.log`
- **Formato**: `[YYYY-MM-DD HH:MM:SS] [NIVEL] [USUARIO] - [STOP4ME] Mensaje`

---

## 👤 Autor

Desarrollado por **DanSanMar** como parte del ecosistema de herramientas de **ALL4ME**.

- **GitHub**: [@DanSanMar](https://github.com/DanSanMar)

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **MIT**. Siéntete libre de modificarlo y adaptarlo a tus necesidades.