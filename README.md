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



## Uso

### Uso de MTKTools con interfaz grafica:

1. Abrir interfaz grafica con el comando de abajo
```
python mtk_gui.py
```
2. Apagar la tablet y conectarla por USB a la computadora (**IMPORTANTE** debe tener el teclado desconectado) mientras presiona los botones de subir y bajar volumen al mismo itempo
3. En la herramienta ve a la pestaña "Read partition(s)" y marca "select all partitions" y haga click en "Read partition(s)", elija una carpeta para guardar los binarios
4. Espere y disfrute de su firmware extraido :)


### Rootear la tablet

1. Primero extraiga el archivo **Boot.img** con el siguiente comando o usando la interfaz grafica
```
python mtk.py r boot boot.img 
```
**Interfaz grafica**
```
python mtk_gui.py 
```

2. Reboot the phone
```
python mtk.py reset
```

3. Download patched magisk for mtk:
Download latest Magisk [here](https://github.com/topjohnwu/Magisk/releases/latest)

4. Install on target phone
- you need to enable usb-debugging via Settings/About phone/Version, Tap 7x on build number
- Go to Settings/Additional settings/Developer options, enable "OEM unlock" and "USB Debugging"
- Install magisk apk
```
adb install app-release.apk
```
- accept auth rsa request on mobile screen of course to allow adb connection

5. Upload boot to /sdcard/Download
```
adb push boot.img /sdcard/Download
```

6. Start magisk, tap on Install, select boot.img from /sdcard/Download, then:
```
adb pull /sdcard/Download/[displayed magisk patched boot filename here]
mv [displayed magisk patched boot filename here] boot.patched
```

7. Do the steps needed in section "Unlock bootloader below"

8. Flash magisk-patched boot
```
python mtk.py w boot boot.patched
```

9. Reboot the phone
```
python mtk.py reset
```

10. Disconnect usb cable and enjoy your rooted phone :)



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




