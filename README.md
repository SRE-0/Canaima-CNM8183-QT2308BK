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

## Informaciòn del dispositivo

- **Modelo**: Tablet **Canaima CNM8183 / QT2308BK**  
- **Firmware identificado**: `cnm8183_v1.0_20240629`  
- **Arquitectura/SoC**: Plataforma **MediaTek 8183**.  
- **Motivación**: preservar el estado **stock**, crear un respaldo verificable y documentar un proceso **reproducible**.

> **Tip**: La verificación del chipset y el mapa de particiones se puede hacer con `mtk printgpt` y registrando VID/PID al conectar en modo BROM. Más abajo te explico cómo.

---

## Requisitos

**SO**:

- **Linux**: probado con Arch Linux (Hyprland / Wayland), Ubuntu y Fedora  
- **Windows**: 10 / 11  (probado en w11)
- **macOS**: 12+

**Software y dependencias**:

- **Python** 3.9+  
- **Git**  
- **libusb/fuse** (en Linux)  
- **Drivers** (Windows: puerto MTK + UsbDk)

---

## Instalación de MTKClient

> Consulta el repo oficil de [MTK Client](https://github.com/bkerler/mtkclient) para su instalacion y uso (CLI/GUI) — proyecto de **bkerler**

## Aspectos legales y descargo de responsabilidad

- Este proyecto es educativo y para preservación del firmware original de tu propio dispositivo.

- No se incluyen imágenes propietarias del fabricante en este repositorio (solo guías, scripts y hashes de verificación).

- No compartas ni distribuyas dumps que contengan identificadores únicos o propiedad intelectual del fabricante sin permiso.

- Tú eres responsable de lo que haces con tu dispositivo. Ni el autor ni colaboradores se hacen responsables de daños, pérdida de datos o bloqueos (brick).

## Créditos y referencias

[MTKClient](https://github.com/bkerler/mtkclient) — Herramienta principal para lectura/escritura en dispositivos MediaTek.

Recursos de aprendizaje y guías de backup/dump en plataformas MTK:

> Si esta guía te sirvió, considera dar **estrella al repo**, abrir Issues con mejoras o PRs con correcciones ✨
---




