# 🧠 Detector de Personalidad con Machine Learning

[![Probar App en Streamlit](https://img.shields.io/badge/🚀%20Probar_App_Streamlit-blue?style=for-the-badge&logo=streamlit)](https://3w6wtv8ae77kaeifny4rxw.streamlit.app/)

## 🎯 Objetivo

Desarrollar un modelo de Machine Learning capaz de predecir si una persona es **introvertida** o **extrovertida** en función de variables conductuales simples, y desplegar una **aplicación interactiva** usando **Streamlit** para facilitar su uso por parte de cualquier usuario.

---

## 🧠 ¿Qué predice este modelo?

La personalidad influye en cómo una persona se relaciona, comunica y actúa en sociedad. Este proyecto explora si es posible predecir el perfil de personalidad mediante información como:

- Tiempo que pasa solo
- Participación social
- Fatiga al socializar
- Presencia digital (posts en redes)
- Cantidad de amigos cercanos

---

## ⚙️ Tecnologías utilizadas

- **Lenguaje**: Python 3.12
- **Librerías principales**:  
  `pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`, `streamlit`, `joblib`
- **Modelos evaluados**:  
  - Regresión Logística  
  - Random Forest  
  - XGBoost  
  - **SVM (modelo final seleccionado)**

---

## 📈 Pipeline del proyecto

1. **Carga y limpieza de datos**
2. **Análisis exploratorio (EDA)**
3. **Ingeniería de variables**
4. **Entrenamiento de múltiples modelos**
5. **Evaluación comparativa**
6. **Selección final (SVM)**
7. **Exportación con `joblib`**
8. **Implementación con Streamlit**

---

## 🔍 Variables utilizadas

| Variable               | Descripción                                      |
|------------------------|--------------------------------------------------|
| `Tiempo_Solo`          | Tiempo promedio que pasa solo                   |
| `Miedo_Escenico`       | Indica si evita hablar en público (0/1)         |
| `Eventos_Sociales`     | Participación en eventos sociales               |
| `Salir`                | Frecuencia de salidas sociales                  |
| `Agotado_Socializar`   | Si se siente agotado tras socializar (0/1)      |
| `Amigos_Cercanos`      | Número de amistades íntimas                     |
| `Frecuencia_Posts`     | Actividad en redes sociales (frecuencia de posts) |

---

## 📊 Evaluación del modelo

Tras entrenar múltiples algoritmos, el modelo final elegido fue **SVM (Support Vector Machine)**, con una buena capacidad de generalización y separación clara entre clases.

**Métricas clave**:
- Accuracy: 0.86
- Precision / Recall balanceado
- ROC AUC: 0.91

Se realizaron validaciones cruzadas y análisis de importancia relativa de las variables.

---

## 🖥️ Aplicación interactiva

👉 [Entrá a la app en Streamlit](https://3w6wtv8ae77kaeifny4rxw.streamlit.app/)

Podés ingresar tus propios datos o simular perfiles para ver si el modelo predice **introversión** o **extroversión**.

Incluye:
- Inputs numéricos y categóricos
- Resultado instantáneo
- Explicación breve del perfil

---

## 🖼️ Vista previa

<p align="center">
  <img src="img/app_preview_1.png" width="600">
</p>

---

## 📂 Estructura del repositorio

