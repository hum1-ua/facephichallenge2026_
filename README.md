# Sistema de Verificación de Identidad para Onboarding Digital

Este proyecto implementa un sistema de verificación de identidad combinando OCR y reconocimiento facial usando [DeepFace](https://github.com/serengil/deepface) y [doctr](https://mindee.github.io/doctr/) para la extracción de texto de documentos. Permite validar información del DNI y verificar que la persona que aparece en el documento coincide con la persona frente a la cámara o en una imagen.

<video src="demo_anti_spoofing.mp4" width="100%" controls></video>

---

## 🔹 Funcionalidades

- **Extracción de datos de DNI:** Lectura automática de datos de anverso y reverso mediante OCR (`doctr`).
- **Validación de datos:** Validación de fechas de nacimiento y validez, así como comprobación de dígito verificador del DNI.
- **Verificación facial en tiempo real:** Comparación de rostro de webcam con foto del DNI usando DeepFace.
- **Verificación one-shot:** Comparación de dos imágenes (DNI vs selfie) sin cámara.
- **Anti-Spoofing:** Detección básica de intentos de suplantación de identidad.
- **Visualización opcional:** Resultados de la verificación se muestran en gráficos y prints con información de coincidencia y distancia coseno.

---

## 🔹 Instalación

Se recomienda crear un entorno virtual:

```bash
py -3.10 -m venv .venv  #se recomienda usar esta versión de python
source .venv/bin/activate      # Linux / macOS
.venv\Scripts\activate         # Windows
```

Instalar dependencias

```bash
pip install -r requirements.txt
```
