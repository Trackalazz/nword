# Propuesta de tareas tras revisión de código

## 1) Corregir error tipográfico
**Problema detectado:** en el README aparece el término "nemotécnica", cuya forma correcta es "mnemotécnica".

**Tarea propuesta:**
- Corregir la palabra en `README.md` para mejorar precisión lingüística y credibilidad del texto.

**Criterio de aceptación:**
- El README no contiene "nemotécnica" y sí "mnemotécnica" en la descripción principal.

---

## 2) Solucionar fallo funcional en el minijuego de definiciones
**Problema detectado:** la validación de respuesta considera correcto un input vacío, porque se evalúa `correctDef.includes(userDef)` y en JavaScript cualquier string incluye `""`.

**Tarea propuesta:**
- Ajustar `checkDefinition` para rechazar explícitamente respuestas vacías antes de aplicar comparaciones flexibles.
- Añadir una condición mínima de longitud/normalización para evitar falsos positivos triviales.

**Criterio de aceptación:**
- Con el campo de definición vacío, la respuesta se marca como incorrecta.
- El resto de casos válidos (coincidencia exacta y coincidencia razonable por palabras clave) se mantiene.

---

## 3) Corregir discrepancia de documentación
**Problema detectado:** el README describe una app muy reducida (solo memorización y caja de comentarios), pero el código incluye carga de archivos (`TXT/RTF/PDF/DOCX`), modos de juego (`nback` y `definitions`) y opciones avanzadas.

**Tarea propuesta:**
- Actualizar `README.md` para reflejar capacidades reales: formatos soportados, modos de juego, configuración de dificultad y flujo básico de uso.
- Incorporar una sección corta de "Formato esperado del diccionario" con ejemplo `palabra: definición`.

**Criterio de aceptación:**
- El README enumera funcionalidades clave presentes en la interfaz/código.
- Un usuario nuevo puede iniciar una sesión sin inspeccionar el código fuente.

---

## 4) Mejorar cobertura de pruebas
**Problema detectado:** no hay pruebas automatizadas para funciones críticas de parsing y validación.

**Tarea propuesta:**
- Introducir pruebas unitarias (extrayendo lógica a funciones testeables) para:
  - `parseDictionary` (líneas válidas, inválidas, múltiples `:`).
  - evaluación de respuestas en definiciones (vacío, exacto, parcial, casos borde).
- Añadir un test de regresión específico para impedir que un input vacío vuelva a contarse como correcto.

**Criterio de aceptación:**
- Existe una suite de pruebas ejecutable en CI/local con casos de éxito y regresión.
- El bug de input vacío queda cubierto por test automático.
