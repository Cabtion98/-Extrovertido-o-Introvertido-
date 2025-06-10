import streamlit as st
import pandas as pd
import joblib
import numpy as np

# ============================
# CONFIGURACIÓN INICIAL
# ============================
st.set_page_config(page_title="Detector de Personalidad", page_icon="🧠", layout="centered")
modelo = joblib.load("modelo_personalidad.pkl")

# ============================
# TÍTULO Y DESCRIPCIÓN
# ============================
st.title("🧠 Detector de Personalidad")
st.markdown("### ¿Introvertido o Extrovertido?")
st.markdown("Descubrí tu perfil de personalidad según tus comportamientos sociales y digitales.")

with st.expander("ℹ️ ¿Qué significa cada rasgo?"):
    st.markdown("""
    - **Introvertido**: Tiende a recargarse estando solo, prefiere interacciones profundas y espacios tranquilos.
    - **Extrovertido**: Se energiza socializando, disfruta de actividades grupales y es más expresivo públicamente.
    """)

st.divider()
st.subheader("📝 Ingresá tus características personales")

# ============================
# FORMULARIO DE ENTRADA
# ============================
col1, col2 = st.columns(2)

with col1:
    tiempo_solo = st.slider("⏱️ Tiempo solo (0 = nada, 10 = todo el día)", 0, 10, 5)
    miedo_escenico = st.selectbox("🎤 ¿Tenés miedo escénico?", ["Sí", "No"])
    salir = st.slider("🏙️ Frecuencia de salidas por semana", 0, 10, 5)

with col2:
    eventos_sociales = st.slider("🎫 Asistencia a eventos sociales", 0, 10, 5)
    agotado = st.selectbox("😫 ¿Te agotás al socializar?", ["Sí", "No"])
    amigos = st.slider("🧑‍🤝‍🧑 Número de amigos cercanos", 0, 20, 5)
    posts = st.slider("📱 Frecuencia de publicaciones en redes", 0, 10, 3)

# ============================
# PREDICCIÓN
# ============================
if st.button("🔮 Predecir personalidad"):
    entrada = pd.DataFrame([{
        "Tiempo_Solo": tiempo_solo,
        "Miedo_Escenico": 1 if miedo_escenico == "Sí" else 0,
        "Eventos_Sociales": eventos_sociales,
        "Salir": salir,
        "Agotado_Socializar": 1 if agotado == "Sí" else 0,
        "Amigos_Cercanos": amigos,
        "Frecuencia_Posts": posts
    }])

    pred = modelo.predict(entrada)[0]
    proba = modelo.predict_proba(entrada)[0]

    st.divider()
    st.subheader("🌟 Resultado del análisis")

    if pred == 1:
        st.success("Sos **Extrovertido 😄**")
    else:
        st.info("Sos **Introvertido 🧘‍♂️**")

    st.metric("Probabilidad de extroversión", f"{proba[1]*100:.2f}%")
    st.metric("Probabilidad de introversión", f"{proba[0]*100:.2f}%")

    # ============================
    # INTERPRETACIÓN PERSONALIZADA
    # ============================
    st.divider()
    st.subheader("🧠 Interpretación personalizada")

    explicacion = []

    if tiempo_solo >= 7:
        explicacion.append("• Pasás mucho tiempo solo, algo característico de personas introspectivas.")
    elif tiempo_solo <= 3:
        explicacion.append("• Te gusta estar acompañado la mayor parte del tiempo.")

    if miedo_escenico == "Sí":
        explicacion.append("• Sentís incomodidad al hablar en público, algo más común en introvertidos.")
    else:
        explicacion.append("• Te desenvolvés bien frente a audiencias, típico de personas extrovertidas.")

    if eventos_sociales <= 3:
        explicacion.append("• Asistís a pocos eventos sociales, lo cual puede indicar preferencia por lo íntimo.")
    elif eventos_sociales >= 7:
        explicacion.append("• Tenés vida social activa, característica extrovertida.")

    if salir <= 3:
        explicacion.append("• Salís poco, probablemente valorás los momentos de calma.")
    elif salir >= 7:
        explicacion.append("• Sos de estar afuera y en movimiento, algo muy sociable.")

    if agotado == "Sí":
        explicacion.append("• Te sentís drenado luego de socializar, rasgo clásico de introversión.")
    else:
        explicacion.append("• Interactuar con otros te recarga, algo habitual en extrovertidos.")

    if amigos <= 3:
        explicacion.append("• Tenés un círculo cercano pequeño, algo común en introvertidos.")
    elif amigos >= 10:
        explicacion.append("• Tenés muchos amigos cercanos, indicio de una red social amplia.")

    if posts <= 2:
        explicacion.append("• Publicás poco en redes, lo cual puede reflejar baja exposición digital.")
    elif posts >= 7:
        explicacion.append("• Sos muy activo en redes sociales, rasgo asociado a extroversión.")

    for frase in explicacion:
        st.write(frase)

    # ============================
    # COMPARACIÓN CON PROMEDIO
    # ============================
    st.divider()
    st.subheader("📊 Comparación con el promedio (simulado)")

    media_simulada = {
        "Tiempo_Solo": 5,
        "Miedo_Escenico": 0.6,
        "Eventos_Sociales": 5,
        "Salir": 5,
        "Agotado_Socializar": 0.5,
        "Amigos_Cercanos": 6,
        "Frecuencia_Posts": 4
    }

    for col in entrada.columns:
        usuario = entrada[col].values[0]
        media = media_simulada[col]
        flecha = "🔺" if usuario > media else "🔻"
        st.write(f"{flecha} **{col}**: Tu valor = {usuario} | Promedio = {media}")

# ============================
# PIE DE PÁGINA
# ============================
st.divider()
st.markdown("Hecho por **Dario Cancelli** | [LinkedIn](https://www.linkedin.com/in/dariocancelli)")