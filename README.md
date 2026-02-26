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
<img width="515" height="427" alt="image" src="https://github.com/user-attachments/assets/8e0b77cc-0f15-4b1e-ae26-e2c6f61216c7" />

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

## Parámetros Configurables

| Parámetro | Descripción |
|-----------|------------|
| `model_name` | Modelo facial (ArcFace recomendado) |
| `detector_backend` | Backend de detección (retinaface recomendado)|
| `threshold` | Umbral de similitud |
| `processing_frame_rate` | Frecuencia de análisis |

---

## Modelos de Reconocimiento Soportados
<img width="3584" height="2008" alt="image" src="https://github.com/user-attachments/assets/67e32be5-db17-48c0-951d-ca1428f542a2" />

## Modelos de detección y alineamiento
<img width="3584" height="2006" alt="image" src="https://github.com/user-attachments/assets/9a2d1fbe-8a24-41d1-8aec-7a9224316abf" />


## Autores
<!-- readme: collaborators -start -->
<table>
<tr>
    <td align="center">
        <a href="https://github.com/hum1-ua">
            <img src="https://avatars.githubusercontent.com/u/198967558?v=4" width="100;" alt="alg204"/>
            <br />
            <sub><b>Adrián</b></sub>
        </a>
    </td>
    <td align="center">
        <a href="https://github.com/ppf30">
            <img src="https://avatars.githubusercontent.com/u/198932016?v=4" width="100;" alt="ppf30"/>
            <br />
            <sub><b>Patricia</b></sub>
        </a>
      </td></tr>
</table>
