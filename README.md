import streamlit as st
import pandas as pd
import mysql.connector
import plotly.express as px

# =========================
# CONFIGURACIÓN
# =========================
st.set_page_config(page_title="Dashboard de Producción", layout="wide")

# =========================
# HEADER PRO (LOGO + TITULO JUNTOS)
# =========================
col1, col2 = st.columns([1,5])

with col1:
    st.image("logo.png", width=700)

with col2:
    st.markdown(
        "<h1 style='color:#00BFFF; margin-bottom:0;'> Dashboard de Producción</h1>",
        unsafe_allow_html=True
    )
    st.markdown(
        "<p style='color:gray; margin-top:0;'>FulfillPro Logística & Fulfillment</p>",
        unsafe_allow_html=True
    )

st.markdown("---")

# =========================
# CONEXIÓN MYSQL
# =========================
conexion = mysql.connector.connect(
    host="localhost",
    user="root",
    password="corona36715",
    database="fulfillment"
)

df = pd.read_sql("SELECT * FROM productividad", conexion)

# =========================
# SIDEBAR FILTROS
# =========================
st.sidebar.title("⚙️ Filtros")

turnos = st.sidebar.multiselect(
    "Selecciona Turno",
    options=df["turno"].unique(),
    default=df["turno"].unique()
)

empleados = st.sidebar.multiselect(
    "Selecciona Empleado",
    options=df["empleado"].unique(),
    default=df["empleado"].unique()
)

# FILTRADO
df = df[
    (df["turno"].isin(turnos)) &
    (df["empleado"].isin(empleados))
]

# =========================
# KPIs
# =========================
total_picking = df["picking"].sum()
total_packing = df["packing"].sum()
total_operaciones = total_picking + total_packing
promedio = total_operaciones / len(df) if len(df) > 0 else 0

col1, col2, col3, col4 = st.columns(4)

col1.metric("📦 Picking Total", total_picking)
col2.metric("📦 Packing Total", total_packing)
col3.metric("⚡ Total Operaciones", total_operaciones)
col4.metric("📊 Promedio por empleado", round(promedio, 2))

st.markdown("---")

# =========================
# GRÁFICAS
# =========================
col1, col2 = st.columns(2)

with col1:
    st.subheader("📊 Productividad por Empleado")
    fig1 = px.bar(
        df,
        x="empleado",
        y=["picking", "packing"],
        barmode="group"
    )
    st.plotly_chart(fig1, use_container_width=True)

with col2:
    st.subheader("📊 Distribución por Turno")
    df_turno = df.groupby("turno").sum(numeric_only=True).reset_index()

    if not df_turno.empty:
        fig2 = px.pie(
            df_turno,
            names="turno",
            values="picking",
            hole=0.4
        )
        st.plotly_chart(fig2, use_container_width=True)
    else:
        st.warning("No hay datos para mostrar")

# =========================
# RANKING
# =========================
st.subheader("🏆 Ranking de Empleados")

df["total"] = df["picking"] + df["packing"]
df_rank = df.sort_values(by="total", ascending=False)

fig3 = px.bar(
    df_rank,
    x="empleado",
    y="total",
    color="total"
)

st.plotly_chart(fig3, use_container_width=True)

# =========================
# ALERTAS
# =========================
st.subheader("🚨 Alertas de Bajo Rendimiento")

if not df.empty:
    promedio_total = df["total"].mean()
    bajo = df[df["total"] < promedio_total]

    if not bajo.empty:
        st.warning("Hay empleados con rendimiento bajo")
        st.dataframe(bajo)
    else:
        st.success("Todos los empleados están dentro del rendimiento esperado")

# =========================
# TABLA FINAL
# =========================
st.subheader("📋 Datos Detallados")
st.dataframe(df)
•	Conexión con sistemas ERP
•	Mejora de interfaz gráfica
•	Implementación en la nube
•	Sistema de usuarios y autenticación
