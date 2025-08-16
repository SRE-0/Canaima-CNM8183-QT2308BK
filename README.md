# Canaima CNM8183 / QT2308BK — Firmware Preservation & Dump Guide

![Project](https://img.shields.io/badge/Project-Firmware_Preservation-5A67D8?style=for-the-badge&logo=github&logoColor=white&labelColor=101010)
![Device](https://img.shields.io/badge/Device-CNM8183_/_QT2308BK-0EA5E9?style=for-the-badge&logo=android&logoColor=white&labelColor=101010)
![Firmware](https://img.shields.io/badge/Firmware-cnm8183__v1.0__20240629-22C55E?style=for-the-badge&logo=buffer&logoColor=white&labelColor=101010)
![Chipset](https://img.shields.io/badge/Platform-MediaTek_MT81xx_(verificar)-F59E0B?style=for-the-badge&logo=mediatek&logoColor=white&labelColor=101010)
![Linux](https://img.shields.io/badge/Linux-Arch_/_Ubuntu_/_Fedora-0DB7ED?style=for-the-badge&logo=linux&logoColor=white&labelColor=101010)
![Windows](https://img.shields.io/badge/Windows-10_/_11-0078D4?style=for-the-badge&logo=windows&logoColor=white&labelColor=101010)
![macOS](https://img.shields.io/badge/macOS-Supported-000000?style=for-the-badge&logo=apple&logoColor=white&labelColor=101010)
![Python](https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white&labelColor=101010)
![MTKClient](https://img.shields.io/badge/Tool-mtkclient-FF6A00?style=for-the-badge&logo=terminal&logoColor=white&labelColor=101010)
![Integrity](https://img.shields.io/badge/Integrity-SHA256_verified-10B981?style=for-the-badge&logo=vercel&logoColor=white&labelColor=101010)
![License](https://img.shields.io/badge/Docs_License-CC_BY_4.0-4B5563?style=for-the-badge&logo=creativecommons&logoColor=white&labelColor=101010)

> **Objetivo**: Preservar el firmware **original** de la Tablet **Canaima CNM8183 / QT2308BK** y explicar de forma clara y reproducible cómo **extraer (dump)** y **verificar** ese firmware utilizando [**MTKClient**](https://github.com/bkerler/mtkclient).

---

## ✨ Contenido

- [Contexto rápido](#-contexto-rápido)
- [Requisitos](#-requisitos)
- [Instalación de MTKClient](#-instalación-de-mtkclient)
- [Preparar el dispositivo (BROM / conexión)](#-preparar-el-dispositivo-brom--conexión)
- [Métodos de respaldo (dump)](#-métodos-de-respaldo-dump)
  - [A) Dump completo en un solo archivo (full flash)](#a-dump-completo-en-un-solo-archivo-full-flash)
  - [B) Dump de **todas** las particiones a carpeta](#b-dump-de-todas-las-particiones-a-carpeta)
  - [C) Dump de particiones específicas](#c-dump-de-particiones-específicas)
- [Verificación de integridad y organización](#-verificación-de-integridad-y-organización)
- [Buenas prácticas de preservación](#-buenas-prácticas-de-preservación)
- [Solución de problemas](#-solución-de-problemas)
- [FAQ](#-faq)
- [Aspectos legales y descargo de responsabilidad](#-aspectos-legales-y-descargo-de-responsabilidad)
- [Créditos y referencias](#-créditos-y-referencias)

---

## 🚦 Contexto rápido

- **Modelo**: Tablet **Canaima CNM8183 / QT2308BK**  
- **Firmware identificado**: `cnm8183_v1.0_20240629`  
- **Arquitectura/SoC**: Plataforma **MediaTek** (el nombre comercial “CNM8183” sugiere familia **MT8183**, **verificar** chipset real en tu unidad).  
- **Motivación**: preservar el estado **stock**, crear un respaldo verificable y documentar un proceso **reproducible**.

> **Tip**: La verificación del chipset y el mapa de particiones se puede hacer con `mtk printgpt` y registrando VID/PID al conectar en modo BROM. Más abajo te explico cómo.

---

## ✅ Requisitos

**Host** (elige tu SO):

- **Linux**: probado con Arch Linux (Hyprland / Wayland), Ubuntu y Fedora  
- **Windows**: 10 / 11  
- **macOS**: 12+

**Software y dependencias**:

- **Python** 3.9+  
- **Git**  
- **libusb/fuse** (en Linux)  
- **Drivers** (Windows: puerto MTK + UsbDk)

**Herramienta principal**:
- **MTKClient** (CLI/GUI) — proyecto de **bkerler**

---

## 🛠 Instalación de MTKClient

> **Linux (Arch / Ubuntu / Fedora)**

```bash
# Arch / Manjaro (paquetes base)
sudo pacman -S python python-pip git libusb fuse2

# Ubuntu/Debian
sudo apt install -y python3 python3-pip git libusb-1.0-0 libfuse2

# Fedora
sudo dnf install -y python3 python3-pip git libusb1 fuse
