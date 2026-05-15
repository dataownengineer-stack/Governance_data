# Estándar de Nomenclatura y Gobierno de Datos  
## Arquitectura Medallón – Proyecto MDM y Gobernanza de Datos "Traza"

**Versión:** 1.0  
**Estado:** Draft  
**Fecha:** Mayo 2026
**Creado por:** Daniel Ruiz

---

# 1. Objetivo

Definir los estándares oficiales de Traza, nomenclatura, segmentación y gobierno de datos para la arquitectura tipo Medallón del proyecto institucional de integración, consolidación y gestión de datos maestros (MDM).

Este documento establece lineamientos para:

- Organización de schemas.
- Nomenclatura de datasets.
- Administración de capas Medallón.
- Estructuras técnicas operativas.
- Homologación de nombres.
- Control y gobernanza de datos.

El objetivo es garantizar:

- Consistencia.
- Escalabilidad.
- Trazabilidad.
- Interoperabilidad.
- Mantenibilidad.
- Calidad de datos.
- Alineación entre equipos técnicos y funcionales.

---

# 2. Alcance

Este estándar aplica para:

- Nuevas integraciones de datos.
- Procesos ETL/ELT.
- Pipelines.
- Cargas masivas.
- Datasets operativos.
- Entidades maestras.
- Procesos MDM.
- Ambientes analíticos.
- Datasets municipales y estatales.

Aplica a todos los motores soportados por la organización:

- PostgreSQL
- MySQL
- Oracle

---

# 3. Referencias y Buenas Prácticas

Este estándar toma como referencia buenas prácticas y lineamientos de:

- ISO 8000 – Calidad de Datos.
- ISO/IEC 11179 – Metadata Registries.
- DAMA-DMBOK.
- Arquitectura Medallón.
- Data Governance Frameworks.
- Mejores prácticas SQL enterprise.
- Convenciones de Data Engineering modernas.

---

# 4. Arquitectura Medallón

La arquitectura Medallón organiza los datos por niveles de madurez y calidad.

El modelo Medallion es una arquitectura de organización de datos que divide la información en capas progresivas de calidad y transformación: Bronze, Silver y Gold. Su objetivo es facilitar la ingestión, limpieza, estandarización y consumo de datos de forma controlada y escalable.

- Bronze: Almacena datos crudos provenientes de los sistemas origen, conservando la información casi sin transformación.
- Silver: Contiene datos depurados, normalizados y consolidados, listos para procesos de integración y análisis.
- Gold: Concentra información de negocio altamente refinada y optimizada para consumo analítico, reportes, indicadores y aplicaciones.

## 4.1 Schemas Oficiales

| Schema | Descripción |
|---|---|
| `bronze` | Datos crudos provenientes de origen |
| `silver` | Datos homologados y estandarizados |
| `gold` | Datos consolidados y listos para consumo |
| `mdm` | Entidades maestras oficiales |
| `ops` | Operación técnica, ETL y control |
| `sandbox` | Exploración y pruebas controladas |

---

# 5. Convención Oficial de Nombres

## 5.1 Reglas Generales

Todos los objetos deberán cumplir obligatoriamente:

- Uso exclusivo de minúsculas.
- Uso obligatorio de `snake_case`.
- Separación mediante guion bajo `_`.
- Prohibido uso de espacios.
- Prohibido uso de acentos.
- Prohibido uso de caracteres especiales.
- Nombres compactos y descriptivos.
- Prohibido uso de sufijos manuales de versión.

---

# 6. Estructura Oficial de Datasets

## 6.1 Datasets Municipales

Formato oficial:

```text
{estado}_{municipio}_{entidad}_{dataset}
```

### Ejemplos

```text
qroo_fcp_cat_predios
qroo_fcp_rpp_propiedades
qroo_fcp_cat_construcciones
```

---

## 6.2 Datasets Estatales

Cuando el dataset pertenezca al nivel estatal y no exista municipio asociado, el componente municipal deberá omitirse.

Formato oficial:

```text
{estado}_{entidad}_{dataset}
```

### Ejemplos

```text
qroo_cat_predios
qroo_rpp_propiedades
```

---

# 7. Catálogo Oficial de Abreviaturas

## 7.1 Estados

| Código | Descripción |
|---|---|
| `ags` | Aguascalientes |
| `bc` | Baja California |
| `bcs` | Baja California Sur |
| `camp` | Campeche |
| `chis` | Chiapas |
| `chih` | Chihuahua |
| `cdmx` | Ciudad de México |
| `coah` | Coahuila |
| `col` | Colima |
| `dgo` | Durango |
| `gto` | Guanajuato |
| `gro` | Guerrero |
| `hgo` | Hidalgo |
| `jal` | Jalisco |
| `mex` | Estado de México |
| `mich` | Michoacán |
| `mor` | Morelos |
| `nay` | Nayarit |
| `nl` | Nuevo León |
| `oax` | Oaxaca |
| `pue` | Puebla |
| `qro` | Querétaro |
| `qroo` | Quintana Roo |
| `slp` | San Luis Potosí |
| `sin` | Sinaloa |
| `son` | Sonora |
| `tab` | Tabasco |
| `tamps` | Tamaulipas |
| `tlax` | Tlaxcala |
| `ver` | Veracruz |
| `yuc` | Yucatán |
| `zac` | Zacatecas |

---

## 7.2 Municipios

| Código | Descripción |
|---|---|
| `bac` | Bacalar |
| `bju` | Benito Juárez |
| `coz` | Cozumel |
| `fcp` | Felipe Carrillo Puerto |
| `imu` | Isla Mujeres |
| `jmm` | José María Morelos |
| `lca` | Lázaro Cárdenas |
| `opb` | Othón P. Blanco |
| `pmo` | Puerto Morelos |
| `sol` | Solidaridad |
| `tul` | Tulum |
---

## 7.3 Entidades

| Código | Descripción |
|---|---|
| `cat` | Catastro |
| `rpp` | Registro Público de la Propiedad |

---

# 8. Convención de Schemas y Ejemplos

## Bronze (`bronze`)

Datos ingestados sin transformación funcional.

### Ejemplos

```sql
bronze.qroo_fcp_cat_predios
bronze.qroo_rpp_propiedades
```

---

## Silver (`silver`)

Datos homologados y normalizados.

### Ejemplos

```sql
silver.qroo_fcp_cat_predios
silver.qroo_rpp_propiedades
```

---

## Gold (`gold`)

Datasets consolidados y orientados a consumo.

### Ejemplos

```sql
gold.qroo_cat_indicadores
gold.qroo_rpp_propiedades_consolidadas
```

---

## MDM (`mdm`)

Entidades maestras institucionales.

### Ejemplos

```sql
mdm.mst_persona
mdm.mst_inmueble
mdm.mst_domicilio
```

---

## OPS (`ops`)

Operación técnica, staging, control y procesamiento ETL.

### Ejemplos

```sql
ops.stg_qroo_fcp_cat_predios
ops.err_qroo_fcp_cat_predios
ops.log_carga_predios
```

---

# 9. Convenciones Técnicas para OPS

## 9.1 Prefijos Técnicos Oficiales

| Prefijo | Significado | Uso |
|---|---|---|
| `stg_` | staging | ingestión inicial |
| `tmp_` | temporal | procesos intermedios |
| `err_` | errores | registros inválidos |
| `log_` | logs | trazabilidad operativa |
| `aud_` | auditoría | seguimiento técnico |
| `wrk_` | working | procesamiento operativo |
| `map_` | mapeos | homologaciones |
| `ref_` | referencia | catálogos técnicos |
| `ctl_` | control | control ETL |
| `qtn_` | quarantine | cuarentena de datos |
| `rec_` | reconciliación | validación origen-destino |
| `his_` | histórico | históricos operativos |
| `bkp_` | respaldo | respaldos temporales |
| `mst_` | master | entidad maestra MDM|


---

# 10. Convenciones para Archivos de Carga

Los archivos de carga deberán mantener alineación con la nomenclatura de datasets.

## Ejemplos

```text
qroo_fcp_cat_predios_20260514_xlsx
qroo_rpp_propiedades_20260514_csv
```

---

# 11. Reglas de Calidad y Gobierno

Todos los datasets deberán cumplir:

- Identificación clara de origen.
- Trazabilidad de carga.
- Control de duplicados.
- Monitoreo de errores.
- Registro de auditoría.
- Validación mínima de calidad.
- Ownership funcional y técnico.


# 11.1 Control de Cargas y Trazabilidad

Con el objetivo de garantizar trazabilidad, auditoría y monitoreo operativo de los procesos de integración de datos, se deberá implementar un conjunto de tablas de control centralizadas dentro del schema `ops`.

Estas tablas permitirán:

- monitorear cargas;
- registrar errores;
- auditar ejecuciones;
- habilitar trazabilidad;
- soportar lineage técnico;
- facilitar troubleshooting;
- controlar reprocesos;
- mantener histórico operativo.

---

# 11.2 Tabla de Control de Cargas

## Nombre Oficial

```sql
ops.ctl_cargas
```

---

## Descripción

Tabla principal para registrar la ejecución y resultado de todas las cargas e ingestiones de datos hacia la arquitectura Medallón.

---

## Estructura Recomendada

| Campo | Tipo Sugerido | Descripción |
|---|---|---|
| `id_carga` | bigint | identificador único de carga |
| `id_lote` | varchar(100) | identificador batch |
| `fecha_inicio` | timestamp | inicio del proceso |
| `fecha_fin` | timestamp | fin del proceso |
| `estado_carga` | varchar(50) | estado del proceso |
| `nivel_capa_destino` | varchar(10) | capa destino |
| `sistema_origen` | varchar(200) | sistema lógico origen |
| `origen_tipo` | varchar(50) | tipo de origen |
| `origen_nombre` | varchar(300) | nombre lógico origen |
| `origen_ruta` | varchar(500) | ip, ruta o ubicación |
| `archivo_nombre` | varchar(300) | nombre archivo |
| `archivo_extension` | varchar(20) | extensión |
| `archivo_peso_mb` | numeric(18,2) | tamaño archivo |
| `schema_destino` | varchar(50) | schema destino |
| `tabla_destino` | varchar(200) | tabla destino |
| `pipeline_nombre` | varchar(200) | pipeline asociado |
| `usuario_proceso` | varchar(100) | usuario/proceso ejecutor |
| `total_registros` | bigint | total registros |
| `registros_ok` | bigint | registros exitosos |
| `registros_error` | bigint | registros inválidos |
| `hash_archivo` | varchar(500) | hash validación |
| `mensaje_error` | text | detalle error |
| `fecha_registro` | timestamp | auditoría técnica |

---

## Valores Recomendados para `estado_carga`

| Valor |
|---|
| `pendiente` |
| `ejecutando` |
| `completado` |
| `error` |
| `cancelado` |
| `reprocesado` |

---

## Valores Recomendados para `origen_tipo`

| Valor |
|---|
| `xlsx` |
| `csv` |
| `txt` |
| `api` |
| `postgresql` |
| `mysql` |
| `oracle` |
| `manual` |

---

## Ejemplo

| Campo | Valor |
|---|---|
| `archivo_nombre` | `predios_fcp_20260514.xlsx` |
| `schema_destino` | `brz` |
| `tabla_destino` | `qroo_fcp_cat_predios` |
| `estado_carga` | `completado` |
| `registros_ok` | `152340` |

---

# 11.3 Tabla de Logs Operativos

## Nombre Oficial

```sql
ops.log_pipeline
```

---

## Descripción

Tabla utilizada para registrar eventos operativos, mensajes técnicos y ejecución de pipelines.

---

## Estructura Recomendada

| Campo | Tipo Sugerido | Descripción |
|---|---|---|
| `id_log` | bigint | identificador log |
| `id_carga` | bigint | referencia carga |
| `fecha_evento` | timestamp | fecha evento |
| `nivel_log` | varchar(20) | nivel severidad |
| `pipeline_nombre` | varchar(200) | pipeline |
| `proceso_nombre` | varchar(200) | proceso |
| `mensaje` | text | detalle |
| `usuario_proceso` | varchar(100) | usuario ejecutor |

---

## Valores Recomendados para `nivel_log`

| Valor |
|---|
| `info` |
| `warning` |
| `error` |
| `debug` |
| `critical` |

---

# 11.4 Tabla de Errores de Registros

## Nombre Oficial

```sql
ops.err_registros
```

---

## Descripción

Tabla para almacenar registros inválidos o rechazados durante procesos ETL/ELT.

---

## Estructura Recomendada

| Campo | Tipo Sugerido | Descripción |
|---|---|---|
| `id_error` | bigint | identificador error |
| `id_carga` | bigint | referencia carga |
| `tabla_destino` | varchar(200) | tabla afectada |
| `registro_origen` | text | contenido original |
| `campo_error` | varchar(200) | campo inválido |
| `tipo_error` | varchar(100) | clasificación |
| `descripcion_error` | text | detalle |
| `fecha_error` | timestamp | fecha evento |
| `usuario_proceso` | varchar(100) | usuario ejecutor |

---

## Valores Recomendados para `tipo_error`

| Valor |
|---|
| `duplicado` |
| `nulo` |
| `longitud` |
| `formato` |
| `catalogo` |
| `integridad` |
| `transformacion` |

---

# 11.5 Tabla de Auditoría de Datasets

## Nombre Oficial

```sql
ops.aud_dataset
```

---

## Descripción

Tabla para registrar cambios estructurales, modificaciones y auditoría funcional sobre datasets.

---

## Estructura Recomendada

| Campo | Tipo Sugerido | Descripción |
|---|---|---|
| `id_auditoria` | bigint | identificador auditoría |
| `schema_nombre` | varchar(50) | schema afectado |
| `tabla_nombre` | varchar(200) | dataset |
| `accion` | varchar(50) | acción realizada |
| `descripcion_cambio` | text | detalle |
| `usuario_cambio` | varchar(100) | usuario responsable |
| `fecha_cambio` | timestamp | fecha modificación |

---

## Valores Recomendados para `accion`

| Valor |
|---|
| `create` |
| `alter` |
| `drop` |
| `rename` |
| `truncate` |
| `reprocess` |

---

# 11.6 Tabla de Reconciliación

## Nombre Oficial

```sql
ops.rec_conciliacion
```

---

## Descripción

Tabla utilizada para validar consistencia entre origen y destino durante procesos de integración.

---

## Estructura Recomendada

| Campo | Tipo Sugerido | Descripción |
|---|---|---|
| `id_reconciliacion` | bigint | identificador |
| `id_carga` | bigint | referencia carga |
| `sistema_origen` | varchar(200) | sistema origen |
| `tabla_origen` | varchar(200) | dataset origen |
| `tabla_destino` | varchar(200) | dataset destino |
| `total_origen` | bigint | total origen |
| `total_destino` | bigint | total destino |
| `diferencia_registros` | bigint | diferencia |
| `estado_reconciliacion` | varchar(50) | resultado |
| `fecha_validacion` | timestamp | fecha |

---

## Valores Recomendados para `estado_reconciliacion`

| Valor |
|---|
| `ok` |
| `warning` |
| `error` |

---

# 11.7 Buenas Prácticas Operativas

## Reglas Obligatorias

- toda carga deberá registrarse en `ops.ctl_cargas`;
- todos los errores deberán almacenarse en `ops.err_registros`;
- todos los pipelines deberán generar logs;
- ningún reproceso deberá sobrescribir históricos;
- todas las cargas deberán tener `id_lote`;
- toda carga deberá registrar usuario o proceso ejecutor;
- los datasets críticos deberán contar con reconciliación;
- toda modificación estructural deberá auditarse.

---

# 12. Reglas de Gobernanza

## 12.1 Altas de Nuevos Datasets

Todo nuevo dataset deberá:

- Registrarse oficialmente.
- Cumplir la nomenclatura.
- Documentar origen.
- Documentar responsable.
- Documentar periodicidad.
- Documentar objetivo funcional.

---

## 12.2 Cambios de Nombre

Queda prohibido renombrar datasets productivos sin:

- Aprobación técnica.
- Validación de impacto.
- Actualización documental.
- Actualización de pipelines dependientes.

---

# 13. Nombres Prohibidos

Queda prohibido el uso de nombres ambiguos, temporales o no controlados.

## Ejemplos Prohibidos

```text
tabla_final
tabla_buena
predios_ok
nuevo_predio
test
test1
tabla2
dataset_final_v2
copia_predios
predios_nuevo_ok
kill
```

---

# 14. Buenas Prácticas Recomendadas

## Recomendaciones Generales

- Mantener nombres cortos y claros.
- Evitar redundancia.
- Reutilizar abreviaturas oficiales.
- Evitar hardcode de versiones.
- Separar datasets funcionales y técnicos.
- Evitar datasets duplicados.
- Documentar cambios estructurales.

---

# 15. Convención Futura para Columnas

Este apartado queda reservado para una fase posterior del proyecto.

Posteriormente se definirán estándares para:

- Llaves primarias.
- Llaves foráneas.
- Timestamps.
- Columnas técnicas.
- Campos booleanos.
- Nomenclatura de identificadores.
- Auditoría funcional QA.
- Estándares MDM.

---

# 16. Ownership y Responsabilidad

Cada dataset deberá tener:

| Tipo | Descripción |
|---|---|
| Responsable funcional | Area dueña del dato |
| Responsable técnico | Area administradora |
| Fuente origen | Sistema fuente |
| Frecuencia | Periodicidad |
| Clasificación | Nivel de sensibilidad |

---

# 17. Ejemplos Integrales

## Ejemplo 1 – Dataset Municipal Bronze

```sql
bronze.qroo_fcp_cat_predios
```

---

## Ejemplo 2 – Dataset Estatal Silver

```sql
silver.qroo_rpp_propiedades
```

---

## Ejemplo 3 – Error Handling

```sql
ops.err_qroo_fcp_cat_predios
```

---

## Ejemplo 4 – MDM Maestro

```sql
mdm.mst_inmueble
```

---

# 18. Consideraciones Finales

El presente estándar tiene como finalidad:

- Facilitar la escalabilidad;
- Mejorar la mantenibilidad;
- Reducir deuda técnica;
- Fortalecer la gobernanza;
- Habilitar trazabilidad y calidad de datos.

Cualquier excepción deberá ser evaluada y aprobada por el equipo de Gobierno de Datos.

---

# 19. Control de Versiones del Documento

| Versión | Fecha | Descripción |
|---|---|---|
| 1.0 | Mayo 2026 | Versión inicial |
