# Auditoría de la Plataforma PAIN

Revisión independiente de **PAIN**, la plataforma que audita la salud digital de
`claro.com.pe`. Este repositorio reúne los entregables de la auditoría y el
material de la revisión anterior.

> **Documento interno.** Contiene la estructura del sistema, resultados de
> pruebas de permisos y vulnerabilidades sin corregir de una plataforma en
> producción. No debe hacerse público.

---

> **Actualizado el 14 de agosto.** Tras cerrarse la auditoría, el equipo entregó
> el diccionario de datos de la plataforma —el plano con el que se migrará la base
> de datos a PostgreSQL—. Auditarlo añadió tres hallazgos y tres trabajos, marcados
> con **✦ Nuevo** en ambos documentos. Lo anterior no cambió.

## Los dos entregables

| Documento | Para qué sirve | Quién lo lee |
|-----------|----------------|--------------|
| **[informe-auditoria.html](informe-auditoria.html)** | Los 28 hallazgos con su evidencia | Dirección y equipo de desarrollo |
| **[plan-de-mejoras.html](plan-de-mejoras.html)** | Los 32 trabajos priorizados, con esfuerzo estimado | Quien planifica |

Se abren con doble clic, no necesitan servidor ni conexión.

**Por qué son dos y no uno.** El informe es una fotografía fechada: es evidencia
y no debe modificarse. El plan es una lista de trabajo viva, que se marca y se
reordena conforme avanza. Mezclarlos obligaría a editar la evidencia.

### Cómo leer el informe

Las secciones **1 a 10** responden qué se auditó, qué se encontró y qué conviene
atender primero. De la **11 en adelante** está la evidencia que sostiene cada
afirmación. Los 28 hallazgos van plegados: se despliegan al pulsarlos, y dentro
de cada uno la evidencia técnica es un segundo nivel.

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

**No se modificó la plataforma.** Todas las pruebas fueron de solo lectura,
salvo el ciclo de vida de datos, que se ejecutó contra un emulador local
sembrado con una copia. El repositorio de la plataforma quedó sin un solo cambio.

---

## Estructura

```
informe-auditoria.html      el informe
plan-de-mejoras.html        el plan de trabajo
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
