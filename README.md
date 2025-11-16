# Auditoría de seguridad para servidores Minecraft 🛡️

Ayudo a owners de **servidores Minecraft pequeños y medianos** a encontrar y corregir fallos de permisos, plugins y configuración para evitar **griefs, robos de rango y exploits**.

---

## 👋 Sobre mí

Soy **David Eros**, admin y técnico de servidores Minecraft especializado en **configuración y seguridad**.

Trabajo con servidores basados en:

- Spigot / Paper / Purpur
- Sistemas de permisos (LuckPerms, etc.)
- Proxies BungeeCord / Velocity
- Plugins típicos como EssentialsX, WorldEdit, etc.

Mi objetivo es ayudarte a que tu servidor sea **más seguro, estable y profesional**, sin que tengas que volverte loco con los detalles técnicos.

---

## 🧩 Servicios que ofrezco

### 🔍 Auditoría básica de seguridad

Revisión rápida para encontrar los fallos más graves:

- Revisión de grupos y permisos (especialmente LuckPerms u otro gestor).
- Detección de permisos peligrosos (`*`, comandos de consola, etc.).
- Revisión rápida de la lista de plugins.
- Señalización de configuraciones inseguras más evidentes.
- Entrega de un **informe corto** con las recomendaciones principales.

> **Pensado para:** servidores pequeños que quieran una primera revisión sencilla.

---

### 🛡️ Auditoría completa de servidor

Análisis más profundo y detallado:

- Revisión extensa de la **estructura de grupos y jerarquía de permisos**.
- Búsqueda de:
  - Rangos con permisos que no deberían tener.
  - Permisos que permiten ejecutar comandos peligrosos.
- Revisión de configuración general:
  - `server.properties`
  - `spigot.yml`, `bukkit.yml`, `paper.yml` (si aplican)
- Detección de:
  - Servidor en `offline-mode` sin protección adecuada.
  - Comandos sensibles accesibles a jugadores (`/plugins`, `/version`, etc.).
- Entrega de un **informe completo**, con:
  - Lista de problemas.
  - Nivel de gravedad (bajo / medio / alto).
  - Explicación del impacto.
  - Soluciones recomendadas.

> **Pensado para:** servidores que quieren tomarse la seguridad en serio y mejorar a medio/largo plazo.

---

### 🧰 Aplicación de soluciones (opcional)

Si no quieres liarte aplicando los cambios tú mismo, puedo ayudarte con:

- Ajuste de permisos en LuckPerms u otro sistema.
- Reorganización de grupos y jerarquía de rangos.
- Reconfiguración básica de plugins clave (EssentialsX, etc.).
- Recomendaciones de estructura de staff y buenas prácticas.

> Esta parte es opcional y se cobra aparte de la auditoría.

---

### 🧪 Plugin de auditoría (en desarrollo)

Estoy trabajando en un **plugin de auditoría para servidores Minecraft** que:

- Revisa grupos y permisos en busca de:
  - Uso del comodín `*`.
  - Comandos de consola accesibles a rangos que no deberían.
  - Permisos peligrosos en rangos “bajos”.
- Analiza la lista de plugins para detectar elementos sospechosos o configuraciones poco seguras.
- Genera un **informe automático** en consola y archivo.

En cuanto tenga una versión estable, la publicaré aquí en este mismo repositorio.

---

## 📂 Casos prácticos (ejemplos reales / de laboratorio)

Estos casos están basados en experiencias reales y en entornos de pruebas que utilizo para detectar problemas típicos en servidores pequeños/medianos.

### Caso 1 – Rango VIP con acceso total al servidor

**Situación:**

Servidor survival con rangos `default`, `vip`, `vip+` y `staff`.  
Los rangos VIP tenían muchos permisos para “dar más cosas” a los jugadores.

**Problema detectado:**

El rango `vip` tenía el permiso `*`, lo que le daba **control total del servidor**:
- Acceso a comandos de administración.
- Capacidad de dar items ilimitados.
- Posibilidad de usar comandos peligrosos de plugins.

**Solución aplicada:**

- Eliminación del permiso `*` del rango VIP.
- Creación de una lista controlada de permisos VIP centrada en:
  - Comandos cosméticos.
  - Comandos de comodidad (homes extra, kits, etc.).
- Revisión de la estructura de grupos en LuckPerms para evitar herencias peligrosas.

**Resultado:**

Se eliminó el riesgo de que un jugador con rango VIP pudiera, de forma intencionada o por error, tomar control completo del servidor.

---

### Caso 2 – Servidor en offline-mode expuesto directamente

**Situación:**

Servidor creativo accesible por IP pública y configurado con `online-mode=false` porque aceptaba jugadores no premium.

**Problema detectado:**

Cualquier usuario podía **suplantar el nombre de otro jugador** (incluso del owner) usando un launcher no premium, entrando con su nick.

**Solución recomendada:**

- Implementación de un proxy (por ejemplo, Velocity) con:
  - Autenticación segura.
  - Protección contra suplantación.
- Bloqueo del acceso directo al backend mediante firewall.
- Mantener el backend en `offline-mode`, pero protegido tras el proxy.

**Resultado:**

Se evitó el riesgo de robos de cuenta, rangos y griefs masivos producidos por suplantación de identidades.

---

### Caso 3 – Jugadores viendo `/plugins` y `/version`

**Situación:**

En un servidor survival, los jugadores del grupo `default` podían usar `/plugins` y `/version`.

**Riesgo:**

- Cualquier jugador podía ver:
  - Lista completa de plugins instalados.
  - Versión exacta del servidor.
- Esto facilita que atacantes busquen **exploits públicos** para esas versiones específicas de plugins o del servidor.

**Solución aplicada:**

- Denegar permisos:
  - `bukkit.command.plugins`
  - `bukkit.command.version`
  al grupo `default`.
- Mantener estos comandos solo accesibles para rangos de administración.

**Resultado:**

Se redujo la cantidad de información sensible disponible para jugadores normales y potenciales atacantes.

---

## ⚙️ Cómo trabajo

1. **Contacto inicial**  
   Hablamos por Discord y me cuentas:
   - Tipo de servidor (survival, skyblock, network, etc.)
   - Si es premium, no premium o mixto.
   - Qué problemas te preocupan más (griefs, rangos, exploits, etc.).

2. **Autorización**  
   Solo trabajo con **permiso explícito** del owner.  
   Siempre que sea posible, hago las pruebas en:
   - Un entorno con whitelist o
   - Una copia del servidor preparada para pruebas.

3. **Revisión técnica**  
   - Analizo grupos y permisos (LuckPerms u otro sistema).
   - Reviso la lista de plugins instalados.
   - Compruebo configuraciones generales (modo online/offline, comandos accesibles, etc.).
   - Si está disponible, ejecuto mi plugin de auditoría.

4. **Informe de resultados**  
   Entrego un informe con:
   - Lista de fallos encontrados.
   - Nivel de gravedad (bajo / medio / alto).
   - Explicación del impacto potencial.
   - Recomendaciones claras para solucionarlo.

5. **Aplicación de cambios (opcional)**  
   Si lo deseas, puedo ayudarte a aplicar las correcciones en:
   - Permisos.
   - Configuraciones.
   - Estructura de rangos y staff.

---

## 💰 Precios orientativos

> Los precios pueden variar según el tamaño del servidor y la complejidad de la configuración.  
> Para cualquier caso concreto, pregúntame por Discord y te doy presupuesto sin compromiso.

**Auditoría básica** – desde **10–15 €**

- Revisión rápida de permisos y plugins.
- Informe corto con los fallos más importantes y cómo arreglarlos.

**Auditoría completa** – desde **25–40 €**

- Análisis detallado de permisos, plugins y configuración general.
- Informe completo con niveles de severidad y pasos concretos para corregirlos.

**Aplicación de soluciones** – desde **+15–25 €** adicionales

- Ajuste de permisos.
- Reconfiguración básica de plugins clave.
- Asesoría en estructura de rangos y staff.

**Métodos de pago habituales:**

- Bizum (si estás en España).
- PayPal.

---

## 📞 Contacto

Si te interesa una auditoría o tienes dudas, puedes contactarme por:

- **Discord:** `TUUSUARIO#0000`
- *(Opcional)* **Email:** `tucorreo@loquesea.com`

Cuando me contactes, puedes mandarme esta info para ir más rápido:

- Tipo de servidor (survival, skyblock, creativo, network, etc.).
- Si es premium/no premium.
- Cuáles son tus preocupaciones principales (seguridad, rangos, exploits, etc.).
