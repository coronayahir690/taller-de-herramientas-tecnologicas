#  Dashboard de Análisis de Datos

##  Descripción

Este proyecto consiste en un dashboard desarrollado en Python utilizando Streamlit para la visualización interactiva de datos.

##  Problema identificado

Las herramientas tradicionales como Excel no permiten una visualización dinámica ni análisis en tiempo real, lo que dificulta la toma de decisiones.

##  Solución

Se desarrolló un dashboard interactivo que permite visualizar datos mediante gráficos, facilitando el análisis y la interpretación de la información.

##  Arquitectura

* Cliente: Navegador web
* Servidor de aplicación: Streamlit (Python)
* Backend: Python
* Base de datos: (opcional, puede integrarse con SQL o ERP)

---

##  Tabla de contenidos

* [Descripción](#-descripción)
* [Problema identificado](#-problema-identificado)
* [Solución](#-solución)
* [Arquitectura](#-arquitectura)
* [Requerimientos](#-requerimientos)
* [Instalación](#-instalación)
* [Configuración](#-configuración)
* [Uso](#-uso)
* [Contribución](#-contribución)
* [Roadmap](#-roadmap)

---

##  Requerimientos

### Servidores

* Servidor local (Streamlit)
* Navegador web

###  Software

* Python 3.8 o superior
* No se requiere Java

###  Paquetes adicionales

* streamlit
* pandas
* matplotlib (opcional)

---

##  Instalación

###  1. Clonar repositorio

git clone https://github.com/coronayahir690/taller-de-herramientas-tecnologicas.git

###  2. Entrar al proyecto

cd taller-de-herramientas-tecnologicas

###  3. Instalar dependencias

pip install -r requirements.txt

---

##  Pruebas manuales

Ejecutar el sistema:
streamlit run panel.py

Verificar:

* Que cargue el dashboard
* Que se muestren los gráficos

---

##  Implementación

###  Local

Se ejecuta mediante Streamlit en localhost:
http://localhost:8501

---

##  Configuración

###  Producto

No requiere configuración adicional.

###  Requerimientos

Instalar librerías necesarias mediante pip.

---

## ▶️ Uso

### Usuario final

1. Ejecutar:
   streamlit run panel.py
2. Abrir navegador
3. Visualizar datos y gráficos

---

###  Administrador

* Modificar el código fuente
* Agregar nuevas visualizaciones
* Integrar nuevas fuentes de datos (ERP, SQL)




## 🛣️ Roadmap

* Integración con bases de datos SQL
* Conexión con sistemas ERP
* Mejora de interfaz gráfica
* Implementación en la nube
* Sistema de usuarios y autenticación
