# Divulgation LaTeX (`divulgation-latex`)

![LaTeX](https://img.shields.io/badge/Language-LaTeX-008080?style=for-the-badge&logo=latex&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-macOS-000000?style=for-the-badge&logo=apple&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)
![Maintenance](https://img.shields.io/badge/Maintained-Yes-green.svg?style=for-the-badge)

Ecosistema modular de plantillas y documentos académicos en LaTeX orientado a presentaciones, memorias técnicas y pósteres científicos para la Universidad Politécnica de Madrid (UPM).

---

## 📌 Dependencia Central: `latex-library`

Este repositorio depende de los paquetes y configuraciones tipográficas centralizadas en [latex-library](https://github.com/EricLuceroGonzalez/latex-library).

Para compilar cualquiera de los documentos en un entorno local, el árbol TeX del sistema debe resolver los paquetes (`.sty` y `.cls`) ubicados en tu directorio de desarrollo:

```bash
# 1. Crear el árbol TDS del usuario (si no existe)
mkdir -p ~/Library/texmf/tex/latex

# 2. Enlazar simbólicamente la librería local
ln -s ~/Developer/tools/latex/Texmf ~/Library/texmf/tex/latex/latex-library
```

El contenido de `~/Developer/tools/latex/Texmf` es un ejempo y es lo más recomendable en entorns Mac, sin embargo cada quien los guarda donde quiera. Los estlos utilizados en estas plantillas usan el las direcciones descritas anteriormente y los estilos se pueden encontrar en el repo [latex-library](https://github.com/EricLuceroGonzalez/latex-library).

> **Verificación:** Ejecuta `kpsewhich UPM_Memoir_Style.sty` (o cualquier estilo de la librería). Debe devolver la ruta absoluta hacia el archivo enlazado.

---

## 📂 Estructura del Repositorio

```text
divulgation-latex/
├── beamer-upm/           # Diapositivas académicas y de divulgación
│   ├── 00-upm-beamer.tex # Archivo raíz de presentación
│   └── contents/         # Módulos temáticos (MUIA, seminarios, reuniones)
│
├── memoir-upm/           # Artículos, notas y memorias estructuradas
│   ├── upm-memoir.tex    # Documento maestro basado en la clase Memoir
│   └── content/          # Capítulos, seminarios y reportes modulares
│
└── poster-upm/           # Formatos de póster científico
    ├── beamer-poster/    # Póster maquetado con Beamer + beamerposter
    └── tcolorbox-poster/ # Póster estructurado con cajas tcolorbox
```

---

## 🛠️ Instrucciones de Compilación

### Opción A: Vía `latexmk` (Recomendado)
El motor resuelve automáticamente todas las pasadas cruzadas de referencias y bibliografía:

```bash
# Para presentaciones Beamer
cd beamer-upm
latexmk -pdf 00-upm-beamer.tex

# Para memorias Memoir
cd ../memoir-upm
latexmk -pdf upm-memoir.tex

# Para pósteres
cd ../poster-upm/tcolorbox-poster
latexmk -pdf poster-upm.tex
```

### Opción B: Inyección temporal con `TEXINPUTS`
Si prefieres compilar sin crear el enlace en `~/Library/texmf`:

```bash
TEXINPUTS=".:$HOME/Developer/tools/latex/Texmf//:" pdflatex 00-upm-beamer.tex
```

---

## 🧹 Limpieza de Archivos Temporales

Para eliminar los archivos auxiliares generados durante la compilación (`.aux`, `.log`, `.fls`, `.fdb_latexmk`):

```bash
latexmk -c
# O manualmente:
rm -f *.aux *.log *.bcf *.run.xml *.fls *.fdb_latexmk *.synctex.gz
```

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.