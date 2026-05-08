# 🚀 SI-Bitacora4-AccesoRemoto: Administrando en la "Nube"

Este repositorio contiene la documentación y configuración de la **Bitácora 4**, centrada en la gestión de servidores remotos, seguridad criptográfica y entornos gráficos distribuidos. 

El objetivo principal es transformar la visión del servidor como una "caja física" a un **servicio en red seguro**, utilizando contenedores Docker para simular una infraestructura real en un centro de datos.

## 📋 Tabla de Contenidos
- [Requisitos Previos](#requisitos-previos)
- [Despliegue de la Infraestructura](#despliegue-de-la-infraestructura)
- [Fase 1: SSH - Forjando la Llave Maestra](#fase-1-ssh---forjando-la-llave-maestra)
- [Fase 2: RDP y Entorno Gráfico](#fase-2-rdp-y-entorno-gráfico)
- [Mapeo de Servicios y Puertos](#mapeo-de-servicios-y-puertos)
- [Solución de Problemas](#solución-de-problemas)
- [Reflexión Final](#reflexión-final)

---

## 🛠️ Requisitos Previos

Antes de comenzar, asegúrate de tener instalado:
* [Docker](https://www.docker.com/) y Docker Compose.
* Un cliente SSH (OpenSSH).
* Un cliente de Escritorio Remoto (MSTSC en Windows o Remmina en Linux).
* Git para el control de versiones.

---

## 🏗️ Despliegue de la Infraestructura

Para garantizar un entorno idéntico y reproducible, hemos utilizado **Docker Compose**.

1.  Crea el directorio de trabajo: `mkdir SI_Bitacora4_TuNombre`.
2.  Dentro de la carpeta, inicia los servicios:
    ```bash
    docker-compose up -d
    ```
3.  Verifica el estado de los contenedores:
    ```bash
    docker ps
    ```

> **Nota:** Deberías ver dos servicios activos: uno para SSH (puerto 2222) y otro para la interfaz gráfica Webtop (puertos 3000 y 3389).

---

## 🔑 Fase 1: SSH - Forjando la Llave Maestra

El acceso por contraseña es vulnerable a ataques de fuerza bruta. Hemos implementado **criptografía de clave pública** utilizando el algoritmo **ED25519**.

### Paso A: Conexión Inicial
Conexión mediante contraseña para verificar visibilidad:
```bash
ssh alumno@localhost -p 2222
# Contraseña: sistemas_informaticos