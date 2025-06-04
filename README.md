# Prueba de Estrategia y Plan de Pruebas para la Aplicación “Andares”

---

## 1. Introducción
El objetivo de este documento es definir un plan de pruebas integral para la aplicación móvil **Andares**, tomando como base los hallazgos documentados en el reporte exploratorio (Reporte de evaluación y defectos encontrados, 7 abr 2025). Además, se incorporarán pruebas adicionales relacionadas con la actualización de versión del SDK y de la propia aplicación, así como controles para asegurar que la aplicación apunte a los ambientes correctos en cada liberación.

---

## 2. Alcance y Objetivos
- **Aplicación bajo prueba (AUT)**: App móvil “Andares” en versión actual; se contemplará también la futura versión con SDK actualizado.  
- **Objetivo principal**:  
  1. Verificar la corrección de los defectos críticos, altos y medios identificados en el testing exploratorio.  
  2. Asegurar cobertura de pruebas funcionales, de integración y no funcionales (UI, rendimiento, seguridad, compatibilidad).  
  3. Validar que la app en nuevas versiones no rompa funcionalidades existentes (testing de regresión).  
  4. Confirmar que la app se conecte siempre al ambiente correcto (desarrollo, pruebas, producción), mitigando el riesgo de apuntar a un entorno equivocado.

---

## 3. Elementos a Probar (Test Items)
A partir del reporte de defectos:

1. **Iconos de redes sociales**
   - Icono “X” redirigiendo a TikTok (DEF-001).

2. **Funcionalidad de buscador**
   - Visualización estable (no desplazamiento de texto) (DEF-002).
   - Bloqueo/crash al seleccionar ciertos resultados (DEF-003).
   - Limpieza de términos (campo “x” para borrar) (DEF-006).
   - Persistencia del buscador al navegar entre pisos (DEF-007).
   - Imágenes asociadas a resultados (no falten imágenes) (DEF-004).

3. **Componentes visuales de la interfaz**
   - Línea no deseada en la pantalla de registro (DEF-005).
   - Campos de entrada:
     - Teléfono: solo dígitos (DEF-008).
     - Validación de formatos de imagen vs. video (DEF-010).

4. **Gestión de perfil**
   - Subida y persistencia de imagen de perfil (DEF-009).

5. **Mejoras sugeridas**
   - Visibilidad de iconos (scroll en buscador y logo).
   - Validación de espacios en campo contraseña.
   - Interacción consistente en selección de género y estado civil.

**Pruebas adicionales por actualización de SDK / versión de la app**
- **Compatibilidad con nuevo SDK**:
  - Verificar que las librerías de terceros (gestión de imágenes, geolocalización, mapas) funcionen sin errores en el SDK actualizado.
  - Probar que la navegación interna (mapas por piso, mapeo de tiendas) no se degrade.

- **Pruebas de regresión**:
  - Críticas: Flujos de alta prioridad (búsquedas, registro, login, visualización de tiendas).
  - Altas/medias: Listados y filtros (nombre de tiendas, horarios, contacto, etc.).

**Pruebas de ambiente**
- Comprobar que la app en cada build apunte al endpoint indicado (QA vs Producción).
- Validar variables de configuración (URLs, claves de API) en configuraciones de entorno.

---

## 4. Tipos de Pruebas y Enfoque

### 4.1 Pruebas Funcionales
- **Casos de Uso Principales**  
  1. **Inicio como invitado / usuario registrado**  
     - Flujo completo: Login → Home → Búsqueda → Resultado → Detalle.  
     - Verificar botones de “Regístrate” y su presentación visual.  
  2. **Registro de usuario**  
     - Validar que campos obligatorios (Nombre, Teléfono, Contraseña) solo acepten datos válidos y muestren mensajes de error apropiados.  
     - Verificación de que el campo *Teléfono* solo acepte dígitos (DEF-008).  
     - Confirmar restricción de espacios en contraseña (Mejora 2).  
     - Probar subida de imagen de perfil:  
       - Subir una imagen válida (jpg/png) → debe guardarse correctamente (DEF-009).  
       - Intentar subir formato no válido (video) → debe rechazarse antes de enviar (DEF-010).  
  3. **Mapa de tiendas por pisos**  
     - Navegación entre pisos → el buscador debe desactivarse automáticamente al cambiar de piso (DEF-007).  
     - Verificar que, al buscar una tienda (Zara, BBVA, Cine, etc.), siempre aparezcan las imágenes (DEF-004).  
     - Confirmar que limpiar la búsqueda (“x”) borra correctamente el término (DEF-006).  
  4. **Búsqueda de íconos de contacto / redes sociales**  
     - En sección “Horarios y contacto”, al tocar iconos:  
       - Icono “X” debe apuntar a Twitter, **no** a TikTok (DEF-001).  
       - Probar iconos de Facebook, Instagram, sitio web… validar cada redirección.  
  5. **Crashes / bloqueos**  
     - Reproducir pasos de DEF-003: al buscar “busca” y seleccionar resultado → la app no debe bloquearse (pantalla en blanco).

### 4.2 Pruebas de Interfaz de Usuario (UI)
- **Consistencia visual y líneas no deseadas**  
  - Revisar que no aparezcan líneas extrañas en pantallas de registro/“Regístrate” (DEF-005).  
  - Verificar la visibilidad de iconos (Mejora 1):  
    - Hacer scroll en pantallas con buscador y logo → íconos no deben “desaparecer” o distorsionarse.  
- **Interacción en selección de género y estado civil**  
  - Asegurar consistencia:  
    - Mostrar lista desplegable correcta, valores seleccionados persisten, estilo uniforme (Mejora 3).

### 4.3 Pruebas de Regresión
- Con cada build posterior al SDK/versión:
  - **Flujo crítico**: Login → Búsqueda → Selección de tienda → Detalle.
  - **Módulos secundarios**:
    - Perfil (edición, cambio de contraseña, subida de imagen).
    - Mapas (carga de pisos, zoom in/out).
    - Búsqueda de horarios y contacto.
    - Navegación de menús laterales / tabs.

### 4.4 Pruebas de Compatibilidad y Dispositivos
- **Versiones de Android/iOS soportadas**:  
  - Mínimo: Android 10 → Último (según políticas de tienda).  
  - iOS 14 → Último.  
  - Probar en al menos:  
    - Móviles de gama baja (RAM 2 GB, CPU mediana).  
    - Móviles de gama alta.  
    - Tablets (si aplica).

- **Resoluciones de pantalla**:  
  - HD (720×1280), FHD (1080×1920), y 2K/3K.

### 4.5 Pruebas de Rendimiento
- **Carga de mapas**  
  - Medir tiempos de carga al cambiar de piso.

- **Tiempo de respuesta en búsquedas**  
  - Buscar “cine”, “BBVA”, “Zara” → validar que resultados aparecen en < 2 segundos.

- **Retardo UI ante interacción intensiva**  
  - Ejecutar búsquedas consecutivas y desplazamientos rápidos.

### 4.6 Pruebas de Seguridad
- **Validación de datos sensibles**  
  - Verificar que contraseña no se almacene en texto plano.  
  - Revisar que llamadas a APIs se realicen sobre HTTPS.

- **Inyección de datos en campos**  
  - Intentar inyección SQL o scripts en campos de búsqueda y formularios (por ejemplo, en Registro o sección de reviews) → la app debe sanitizar entradas.

### 4.7 Pruebas de Ambientes y Configuración
- **Verificación de endpoints**  
  - En **build QA**: apuntar a `https://qa.andares.example.com`  
  - En **build Producción**: apuntar a `https://api.andares.example.com`  

  **Procedimiento**:
  1. Configurar archivo de configuración (por ejemplo, `config.json` o variables de entorno) para cada ambiente.  
  2. Desplegar build en QA → validar mediante logs o interceptación de tráfico (Charles/Fiddler) que el endpoint es correcto.  
  3. Desplegar build en Producción → validar de la misma forma.  
  4. **Prueba negativa**: cambiar intencionalmente a un ambiente inexistente (por ejemplo, “staging-noexiste”) → la app debe arrojar error controlado (mensaje de “Servicio no disponible”).

- **Pruebas de migración de versiones**  
  - Verificar que, al instalar la app sobre una versión anterior (mismo dispositivo), los datos de usuario (token, perfil) se conserven o migren correctamente sin corromperse.  
  - Instalar en limpio → flujos nuevos.

---

## 5. Entorno de Pruebas

| Componente               | Descripción                                                                                  |
|--------------------------|----------------------------------------------------------------------------------------------|
| Dispositivos Android     | Android 10, Android 12, Android 14 (físicos o emuladores).                                   |
| Dispositivos iOS         | iOS 14, iOS 16 (físicos o simuladores).                                                       |
| Servidor QA              | `https://qa.andares.example.com` (base de datos, servicios REST).                            |
| Servidor Producción      | `https://api.andares.example.com`                                                             |
| Herramientas de prueba   | • Appium (para automatización móvil)  
                            • Charles/Fiddler (monitoreo de tráfico)  
                            • Postman (pruebas de API)  
                            • Android Studio / Xcode (emuladores)                     |
| Gestión de defectos      | Jira (proyecto “ANDARES-QA”)                                                                 |
| Repositorio de código    | GitHub – rama `release/andares-vX.Y.Z`                                                        |
| Build Automation         | Jenkins pipeline que genera APK/IPA por rama                                                  |

---

## 6. Cronograma de Pruebas (Ejemplo)

| Fase                     | Actividad                                                                  | Duración Estimada |
|--------------------------|----------------------------------------------------------------------------|-------------------|
| Planificación            | Revisar reporte exploratorio; preparar casos de prueba; configurar entornos. | 2 días            |
| Ejecución Inicial        | Pruebas funcionales sobre versión actual.                                   | 3 días            |
| Análisis de Anomalías    | Registrar defectos críticos y altos; coordinar con Desarrollo correcciones. | 1 día             |
| Ciclo de Regresión 1     | Validar fixes; volver a ejecutar flujos críticos.                           | 2 días            |
| Pruebas de Compatibilidad| Ejecutar en dispositivos/OS distintos.                                      | 2 días            |
| Pruebas de Rendimiento   | Medir tiempos de respuesta (búsquedas, mapas).                               | 1 día             |
| Validación de Entornos   | Verificar apuntado a QA/Producción según build.                              | 1 día             |
| Revisión Final           | Reporte final de estatus, lecciones aprendidas.                              | 1 día             |
| **Total Aproximado**     | **~12 días hábiles**                                                          |                   |

> **Nota**: Los días pueden ajustarse según gravedad de defectos y disponibilidad de recursos.

---

## 7. Riesgos y Mitigaciones

| Riesgo                                                                          | Probabilidad | Impacto       | Mitigación                                                                                                                 |
|---------------------------------------------------------------------------------|--------------|---------------|----------------------------------------------------------------------------------------------------------------------------|
| La app apunta al **ambiente equivocado** (QA en producción, o viceversa)       | Media        | Crítico       | • Incluir pruebas automáticas que validen el endpoint en cada build.  
                                                                                      • Configurar pipeline para fail build si URL maligna. |
| **Defectos críticos no cubiertos** durante el testing exploratorio              | Baja-Media   | Alto          | • Priorizar pruebas automatizadas para flujos críticos (búsquedas, login, mapas).  
                                                                                      • Revisar diariamente backlog de defectos. |
| Incompatibilidad con el **nuevo SDK** (p. ej., errores de librerías de terceros) | Media        | Alto          | • Probar early build con SDK actualizado y revisar logs detallados.  
                                                                                      • Mantener board con issues de integración. |
| **Falta de datos de prueba** realistas                                           | Media        | Medio         | • Preparar dataset con tiendas, horarios y múltiples escenarios (sin imagen, con imagen, con datos corruptos).             |
| **Sobrecarga de performance** al tener muchos usuarios simultáneos en mapas      | Baja         | Medio-Alto    | • Ejecutar pruebas de carga ligeras en “QA Performance” antes de liberación.                                               |
| Usuarios finales pierden datos de perfil (imagen) tras update                     | Baja         | Medio-Alto    | • Probar migración de datos entre versiones en dispositivos reales.  
                                                                                      • Validar backup/restauración de datos. |

---

## 8. Criterios de Entrada y Salida

### Criterios de Entrada (para comenzar pruebas)
1. Versión de la app generada y desplegada en ambiente QA.  
2. Entorno QA configurado con base de datos de prueba y servicios disponibles.  
3. Casos de prueba escritos y revisados.  
4. Herramientas de prueba (Appium, Charles, etc.) instaladas y configuradas.  
5. Datos de prueba (usuarios, tiendas, imágenes) cargados en QA.

### Criterios de Salida (para concluir pruebas)
1. Todos los defectos críticos y altos identificados y validados en fixes (cerrados o backlog).  
2. Cumplimiento mínimo del **90 %** de casos de prueba ejecutados.  
3. Reporte de cobertura de pruebas (funcionales + no funcionales).  
4. Aprobación formal de QA Lead para liberación a Producción.  
5. Documentación de lecciones aprendidas y checklist de puntos de control (incluyendo validación de ambiente correcto).

---

## 9. Entregables de Prueba
- **Plan de Pruebas** (este documento).  
- **Conjunto de Casos de Prueba** (detallados en Excel o herramienta de gestión).  
- **Registro de Ejecución** (logs de Appium, capturas de pantalla de errores, grabaciones de video cuando aplique).  
- **Informe de Defectos** en Jira (con prioridad, pasos, evidencia).  
- **Reporte de Cobertura y Métricas** (porcentaje de casos ejecutados y porcentaje de éxito).  
- **Checklist de Entornos** (validación de endpoints, variables de configuración).  
- **Reporte de Resultados de Performance** (tiempos medios de carga de vistas críticas).  
- **Informe Final de QA** (resumen ejecutivo, estado de calidad, recomendaciones para despliegue).

---

## 10. Conclusiones
- Con base en los defectos críticos y altos hallados en el testing exploratorio, es indispensable priorizar la corrección de:
  1. **Crash al seleccionar resultados (“busca”)** (DEF-003).  
  2. **Icono de Twitter redirigiendo a TikTok** (DEF-001).  
  3. **Persistencia no deseada del buscador** (DEF-007).  
  4. **Problemas de imágenes faltantes en búsquedas** (DEF-004).  
  5. **Campo teléfono aceptando caracteres no numéricos** (DEF-008).  
  6. **Subida de imagen de perfil que no persiste** (DEF-009).

- La actualización de la versión del SDK y de la app exige pruebas de regresión y compatibilidad para asegurar que nuevos cambios no introduzcan regresiones en funcionalidades existentes.  
- Es crítico establecer un proceso automatizado que valide, en cada pipeline, que la app apunte al ambiente correcto. La omisión de este punto en versiones anteriores ocasionó un incidente grave en producción.
