# Segmentación de glotis (YOLO + S3AR-UNet)

Este repositorio contiene notebooks para entrenar y ejecutar segmentación de glotis en video usando:
- **YOLO** para localizar una **región de interés (ROI)**
- **S3AR-UNet** para segmentar la glotis

---

## Estructura del repositorio

- `model/`
  - `SeARUNet-2_sin_ROI`: pesos del modelo entrenado con **frames completos**
  - `SeARUNet-3_roi_1.1/`: pesos del modelo entrenado con **frames recortados**
  - `yolo`: pesos de yolo para el roi
- Notebooks:
  - `S3AR_UNet.ipynb` → entrenamiento / arquitectura (principal)
  - `predict_s3ar_unet.ipynb` → inferencia sobre video y generación de salida
  - `S3AR_UNet-Copy1.ipynb` → copia
  - 
---
## Dos pipelines en el archivo de predicción:
### Segmentación en frame completo + filtrado con ROI YOLO
1) YOLO obtiene la ROI global del video.  
2) Para cada frame **completo**, S3AR-UNet segmenta.  
3) Se filtra la máscara usando la ROI (se elimina segmentación fuera de la zona).  
4) Se dibujan contornos sobre el **video completo** (misma resolución).

### Segmentación directa sobre ROI recortada con YOLO
1) YOLO obtiene la ROI global del video.  
2) Cada frame se **recorta** usando esa ROI.  
3) S3AR-UNet segmenta **solo el recorte**.  
4) Se dibujan contornos sobre el **video recortado** (salida recortada).




---
