# Sistema de Verificación de Identidad para Onboarding Digital

Este proyecto implementa un sistema de verificación de identidad combinando OCR y reconocimiento facial usando [DeepFace](https://github.com/serengil/deepface) y [doctr](https://mindee.github.io/doctr/) para la extracción de datos de documentos. Permite validar información del DNI y verificar que la persona que aparece en el documento coincide con la persona frente a la cámara o en una imagen.

##  Demo
[!](https://github.com/user-attachments/assets/c1c06fd9-2776-4211-8cf0-a019d947f9de)

---

##  Funcionalidades

### 1. Validación de DNI (OCR)
- Lectura automática de anverso y reverso
- Extracción de:
  - Nombre y apellidos
  - Fecha de nacimiento
  - Fecha de validez
  - Número de DNI
- Validación de:
  - Dígito verificador
  - Coherencia entre anverso y reverso
  - Caducidad del documento

### 2. Verificación Facial One-Shot
- Comparación DNI vs selfie
- Métrica de distancia coseno
- Configurable:
  - Modelo (ArcFace, Facenet, VGG-Face…)
  - Backend de detección (retinaface, mtcnn, opencv…)

### 3. Verificación en Tiempo Real
- Captura por webcam
- Procesamiento cada N frames (optimización rendimiento)
- Umbral configurable
- Visualización en pantalla completa
- Indicadores:
  - 🟢 MATCH
  - 🔴 NO MATCH
  - 🛑 Spoofing Detected

### 4. Anti-Spoofing
- Detección básica de intentos de suplantación
- No muestra distancia si se detecta spoofing
- Previene ataques con foto en pantalla

### 5. Verificación de edad
- Cálculo de la edad a partir de la fecha de nacimiento del DNI.
- Estimación de edad mediante análisis facial.
- Comparación entre ambas para detectar posibles inconsistencias.
---

##  Arquitectura del Sistema

```
Imagen DNI → OCR → Extracción de datos → Validaciones internas
                             ↓
                       Embedding facial
                             ↓
                 Comparación con selfie/webcam
                             ↓
                  Resultado de verificación
```

---

## Instalación

Se recomienda usar **Python 3.10**.

### 1️. Crear entorno virtual

```bash
py -3.10 -m venv .venv
```

Activar entorno:

Linux / macOS:

```bash
source .venv/bin/activate
```

Windows:

```bash
.venv\Scripts\activate
```

### 2. Instalar dependencias

```bash
pip install -r requirements.txt
```
---

## Uso

### Validación de DNI

```python
validar_dni("dni_anverso.jpg", "dni_reverso.jpg", verificar_edad=True)
```
Ejemplo de salida:
```bash
DNI MODERNO
El dni coincide
El num_sop coincide
La fecha de nacimiento coincide
La fecha de validez coincide
El primer apellido coincide
El segundo apellido coincide
El primer nombre coincide
El segundo nombre coincide (no presente en ambos)
Edad según el DNI: 20
Edad estimada por el modelo: 39
POSIBLE INCONSISTENCIA DE EDAD
```


### Verificación One-Shot

```python
one_shot_verification(
    dni_path="dni.jpg",
    selfie_path="selfie.jpg",
    model_name="ArcFace",
    detector_backend="retinaface"
)
```
<img width="515" height="427" alt="image" src="https://github.com/user-attachments/assets/ed2c2db9-77bf-424e-a4a9-6e469164599c" />
### Verificación en Tiempo Real

```python
real_time_verification(
    dni_path="dni.jpg",
    model_name="ArcFace",
    detector_backend="retinaface"
)
```

Salir con:

```
q
```

---

## ⚙️ Parámetros Configurables

| Parámetro | Descripción |
|-----------|------------|
| `model_name` | Modelo facial (ArcFace recomendado) |
| `detector_backend` | Backend de detección |
| `threshold` | Umbral de similitud |
| `processing_frame_rate` | Frecuencia de análisis |

---

## 🧠 Modelos Soportados (DeepFace)

- ArcFace (recomendado)
- Facenet
- Facenet512
- VGG-Face
- DeepID
- Dlib

---

## 🔐 Consideraciones de Seguridad

- No subir imágenes reales de DNI a repos públicos.
- Usar almacenamiento cifrado en producción.
- Ajustar umbral según entorno real.
- Implementar liveness detection avanzada para uso comercial.

---

## 📚 Tecnologías Utilizadas

- DeepFace
- Doctr OCR
- OpenCV
- TensorFlow
- NumPy
- Matplotlib

---

## 🎯 Posibles Mejoras

- Liveness detection avanzada (parpadeo, movimientos)
- API REST con FastAPI
- Interfaz web
- Dockerización
- Deploy en cloud

---

## Estado del Proyecto

Proyecto educativo enfocado a sistemas de onboarding digital y verificación biométrica.

---

## Autores

Patricia Pérez Ferre
Hugo Urbán Martínez


---

## 📄 Licencia

Uso educativo y demostrativo.
No apto para producción sin mejoras de seguridad.t="image" src="https://github.com/user-attachments/assets/fc64cdcf-6a3f-4bb1-bb54-5e8e7a5e9219" />

