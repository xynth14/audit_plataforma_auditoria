# Auditoría de la Plataforma PAIN

Revisión independiente de **PAIN**, la plataforma que audita la salud digital de
`claro.com.pe`. Este repositorio reúne los entregables de la auditoría y el
material de la revisión anterior.

> **Documento interno.** Contiene la estructura del sistema, resultados de
> pruebas de permisos y vulnerabilidades sin corregir de una plataforma en
> producción. No debe hacerse público.

---

> **Actualizado el 17 de setiembre.** Al añadir filtros a las tarjetas de resumen
> de cada módulo hubo que comprobar, módulo por módulo, que el número de la
> tarjeta y las filas de la tabla salieran del mismo sitio. De ahí sale un cuarto
> documento, **[revision-plataforma-2026-09.html](revision-plataforma-2026-09.html)**,
> con 8 puntos donde el dato que se calcula y el que se muestra no coinciden.
> Todos medidos sobre la colección MVP 200 Urls. Lo anterior no cambió.

> **Actualizado el 25 de agosto.** El cliente pidió auditar la plataforma con la
> resolución de un Galaxy Fold —el dispositivo desde el que se reportó que el
> sitio se rompe— y extender la prueba a otras resoluciones poco frecuentes. Sale
> de ahí un tercer entregable, **[informe-resoluciones.html](informe-resoluciones.html)**,
> con 10 hallazgos propios. Dos ya están corregidos y verificados. Lo anterior no
> cambió.

> **Actualizado el 14 de agosto.** Tras cerrarse la auditoría, el equipo entregó
> el diccionario de datos de la plataforma —el plano con el que se migrará la base
> de datos a PostgreSQL—. Auditarlo añadió tres hallazgos y tres trabajos, marcados
> con **✦ Nuevo** en ambos documentos. Lo anterior no cambió.

## Los cuatro entregables

| Documento | Para qué sirve | Quién lo lee |
|-----------|----------------|--------------|
| **[informe-auditoria.html](informe-auditoria.html)** | Los 28 hallazgos con su evidencia | Dirección y equipo de desarrollo |
| **[plan-de-mejoras.html](plan-de-mejoras.html)** | Los 32 trabajos priorizados, con esfuerzo estimado | Quien planifica |
| **[informe-resoluciones.html](informe-resoluciones.html)** | Los 10 hallazgos de resoluciones poco comunes, con el antes y el después de lo corregido | Dirección y equipo de desarrollo |
| **[revision-plataforma-2026-09.html](revision-plataforma-2026-09.html)** | Los 8 puntos donde el dato calculado y el mostrado no coinciden, con capturas de cada caso | Equipo de desarrollo |

Se abren con doble clic, no necesitan servidor ni conexión.

**Por qué el informe y el plan van separados.** El informe es una fotografía
fechada: es evidencia y no debe modificarse. El plan es una lista de trabajo
viva, que se marca y se reordena conforme avanza. Mezclarlos obligaría a editar
la evidencia.

### Cómo leer el informe

Las secciones **1 a 10** responden qué se auditó, qué se encontró y qué conviene
atender primero. De la **11 en adelante** está la evidencia que sostiene cada
afirmación. Los 28 hallazgos van plegados: se despliegan al pulsarlos, y dentro
de cada uno la evidencia técnica es un segundo nivel.

### Cómo leer el informe de resoluciones

Empieza por **«En una página»**, que resume la causa del fallo reportado y lo que
se hizo con ella. La sección **3** aísla el caso del Galaxy Fold en sus cuatro
estados; la **4** lleva los 10 hallazgos; la **7** deja las 84 medidas en crudo
para quien quiera comprobarlas.

Los hallazgos corregidos **conservan su evidencia original** y se les añade qué
se cambió y qué dio la nueva medición. Nada se marca como resuelto sin haberlo
vuelto a medir: la línea base se regeneró restaurando los archivos originales y
corriendo la auditoría otra vez.

---

## Qué se auditó

| Frente | Alcance |
|--------|---------|
| Interfaz | 20 direcciones × 3 dispositivos × 3 roles |
| API | 66 operaciones de lectura + 44 pruebas con datos inválidos |
| Permisos | 28 operaciones de escritura contra los 3 roles |
| Datos | Ciclo completo de alta, edición y borrado sobre una copia aislada |
| Catálogo | Las 177 reglas cruzadas contra el código y contra 167 375 hallazgos |
| Diccionario de datos | Las 34 tablas y 713 columnas del plano de migración, contrastadas contra el esquema real |
| Código | Dependencias, vulnerabilidades conocidas, pruebas automatizadas |
| Resoluciones | 12 resoluciones × 7 pantallas = 84 medidas, más las 18 tablas del visor y las 7 cabeceras de gestión |

**Las auditorías no modificaron la plataforma.** Todas las pruebas fueron de solo
lectura, salvo el ciclo de vida de datos, que se ejecutó contra un emulador local
sembrado con una copia. Durante la medición se bloquearon a nivel de red todas
las operaciones de escritura.

**Las correcciones vinieron después, y son dos.** Cerrada la medición se corrigió
la cabecera que no se plegaba —que arrastró consigo el incumplimiento de reflow
de WCAG 1.4.10— y se plegaron las columnas constantes de las tablas del visor.
El informe de resoluciones documenta ambas con su medición de antes y de después,
y de cada archivo tocado se conservó copia del original. **Esos cambios no forman
parte de este repositorio:** aquí solo están los informes.

---

## Estructura

```
informe-auditoria.html      el informe
plan-de-mejoras.html        el plan de trabajo
informe-resoluciones.html   el informe de resoluciones poco comunes
out/capturas/               las 54 capturas que ilustran el informe
ux_audit_lectura/           revisión anterior (agosto 2026), solo lectura
```

### `ux_audit_lectura/`

Material de la **primera revisión**, hecha desde fuera y sin acceso al código
fuente. Se conserva porque el informe actual la reconcilia hallazgo por hallazgo:
cuatro de sus siete observaciones ya están corregidas, y la sección
«Reconciliación con la auditoría previa» documenta cuáles y con qué evidencia.

Sus scripts no están pensados para ejecutarse desde aquí: faltan sus
dependencias y su archivo de credenciales, que nunca se versionó.

---

## Qué NO está en este repositorio

- **Credenciales.** Ningún archivo `.env`, ni claves, ni contraseñas.
- **Volcados de datos de producción.** La evidencia cruda con datos personales
  se quedó fuera a propósito.
- **Los generadores de los informes.** Los documentos se entregan renderizados;
  el instrumental de la auditoría no forma parte del entregable.
- **Los cambios hechos en la plataforma.** Las correcciones descritas en el
  informe de resoluciones se aplicaron sobre el código de la plataforma, que
  tiene su propio repositorio. Aquí queda su medición, no su código.
