# Estándar de Nomenclatura y Gobierno de Datos  
## Arquitectura Medallón – Proyecto MDM y Gobernanza de Datos

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
| `qroo` | Quintana Roo |

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
qroo_fcp_cat_predios_20260514.xlsx
qroo_rpp_propiedades_20260514.csv
```

---

# 11. Reglas de Calidad y Gobierno

Todos los datasets deberán cumplir:

- identificación clara de origen;
- trazabilidad de carga;
- control de duplicados;
- monitoreo de errores;
- registro de auditoría;
- validación mínima de calidad;
- ownership funcional y técnico.

---

# 12. Reglas de Gobernanza

## 12.1 Altas de Nuevos Datasets

Todo nuevo dataset deberá:

- registrarse oficialmente;
- cumplir la nomenclatura;
- documentar origen;
- documentar responsable;
- documentar periodicidad;
- documentar objetivo funcional.

---

## 12.2 Cambios de Nombre

Queda prohibido renombrar datasets productivos sin:

- aprobación técnica;
- validación de impacto;
- actualización documental;
- actualización de pipelines dependientes.

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
```

---

# 14. Buenas Prácticas Recomendadas

## Recomendaciones Generales

- mantener nombres cortos y claros;
- evitar redundancia;
- reutilizar abreviaturas oficiales;
- evitar hardcode de versiones;
- separar datasets funcionales y técnicos;
- evitar datasets duplicados;
- documentar cambios estructurales.

---

# 15. Convención Futura para Columnas

Este apartado queda reservado para una fase posterior del proyecto.

Posteriormente se definirán estándares para:

- llaves primarias;
- llaves foráneas;
- timestamps;
- columnas técnicas;
- campos booleanos;
- nomenclatura de identificadores;
- auditoría funcional;
- estándares MDM.

---

# 16. Ownership y Responsabilidad

Cada dataset deberá tener:

| Tipo | Descripción |
|---|---|
| Responsable funcional | área dueña del dato |
| Responsable técnico | área administradora |
| Fuente origen | sistema fuente |
| Frecuencia | periodicidad |
| Clasificación | nivel de sensibilidad |

---

# 17. Ejemplos Integrales

## Ejemplo 1 – Dataset Municipal Bronze

```sql
brz.qroo_fcp_cat_predios
```

---

## Ejemplo 2 – Dataset Estatal Silver

```sql
slv.qroo_rpp_propiedades
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

- facilitar la escalabilidad;
- mejorar la mantenibilidad;
- reducir deuda técnica;
- fortalecer la gobernanza;
- habilitar trazabilidad y calidad de datos.

Cualquier excepción deberá ser evaluada y aprobada por el equipo de Gobierno de Datos.

---

# 19. Control de Versiones del Documento

| Versión | Fecha | Descripción |
|---|---|---|
| 1.0 | Mayo 2026 | Versión inicial |
