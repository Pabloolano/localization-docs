# Reportes e Impuestos DGI

Módulo `l10n_uy_tax_reports`. Camino operativo bajo `Contabilidad → Uruguay → Impuestos`:

| Menú | Para qué |
|------|----------|
| **Liquidación Mensual y Boleto de Pago** | **Camino principal:** calcular/aprobar liquidadores → DJ 1376 → boleto → asientos → candado; botón **TXT DGI (PADI)** |
| **Liquidadores** | Detalle por impuesto (debug / revisión); aprobar exige grupo Aprobador |
| **Formularios DGI** | Consulta TXT 2181/1146 y detalle DJ 1376. La DJ **no** se calcula ni aprueba aquí: usar la liquidación del mes |

Los ítems se muestran según los tildes de **Impuestos UY** en la compañía.

El **1376** se arma desde el pack; el detalle del IVA se mira en **Liquidadores → IVA**.

![Menú Uruguay: diferencia de cambio y reportes DGI](img/odoo-menu-uruguay.jpg)

El filtro de diarios en Ajustes es **opcional**: vacío = todos. Si se carga, acota **TXT y 1376** a esos diarios. La liquidación sigue dependiendo del mapeo de cuentas e impuestos. La diferencia de cambio **Gravada (IVA)** alimenta el 2181: corré ese cálculo antes del mes.

---

## Antes de calcular

En `Contabilidad → Configuración → Ajustes` (compañía fiscal Uruguay), bloque **Impuestos UY** (también pestaña en la ficha de la compañía):

1. Qué impuestos habilitar (IVA, IRAE, Patrimonio/IPAT, …).
2. **Diarios para Reportes DGI** — filtro opcional (vacío = todos). Aplica a **TXT y DJ 1376** por igual.
3. Cuentas y parámetros de liquidación: diario de cierre, DGI a pagar, IVA/excedente/OTT, anticipos IRAE/IP/ICOSA, IRPF, importación. Sin diario de cierre no se pueden generar asientos desde **Liquidación del mes**.
4. Si **no hay ejercicio fiscal cerrado anterior** en Odoo, Ajustes muestra un aviso y campos para cargar a mano el **% / coeficiente de anticipo IRAE (renta)** y el de **Patrimonio / IPAT** (base anual × coeficiente, p. ej. 1/12 ≈ 0,0833; o importe fijo mensual).

**Patrimonio (IPAT)** es una sola familia fiscal, no dos impuestos distintos:

| Dónde | Qué |
|-------|-----|
| Ajustes / compañía | Un bloque: anticipo **mensual** (1376/boleto) + determinación **anual** + DJ **1050** |
| Liquidadores → **Patrimonio (IPAT)** | Submenú **Anticipo mensual** / **Determinación anual** |
| Formularios DGI → **1050 — Patrimonio anual** | Pack anual (exige determinación aprobada). Tras «formulario listo» / cerrar: **propuestas** de coef/mín IRAE, IPAT e ICOSA en el hub; viven en el 1376 solo con **Aplicar propuestas al hub** (Aprobador). No sustituye la confección PADI del 1050. |

**Crédito / excedente IVA inicial (cutover):** en Impuestos UY cargá el L21 de arranque (semilla). Se usa **solo** si no hay DJ 1376 del mes anterior **aprobada**; después manda la cadena mes a mes. No es el saldo eterno de la cuenta 114310 (esa puede servir de control, no de dueña del número).

En el liquidador **IVA** y en la liquidación del mes se muestra **Saldo IVA a favor**. Si no hay IVA a pagar, en **Boletos** queda una línea informativa `IVA: $0 — crédito a favor …` (sin exigir nº/PDF de boleto).

En cada impuesto (`Contabilidad → Configuración → Impuestos`):

| Campo | Para qué |
|-------|----------|
| Línea 2181 | Agrupa el tax en el 2181 |
| Línea 2183 | Agrupa el tax en el 2183 (agente) |
| Línea 1146 | Agrupa el tax en el 1146 |
| Línea 1144 | Agrupa el tax en el 1144 (dependientes / IRPF tipado) |
| Categoría DJ 1376 (venta) | Clasifica ventas de la liquidación |
| Tipo IVA compras 1376 | Clasifica compras de la liquidación |

Si el tax no está mapeado, el XML CFE puede estar bien y el reporte igual sale incompleto.

---

## Liquidadores (detalle por impuesto)

`Contabilidad → Uruguay → Impuestos → Liquidadores → …`

Ahí se calcula y aprueba cada impuesto del mes (montos a pagar / crédito). Es el lugar del **detalle de liquidación** (p. ej. IVA), no el armado del boleto.

En el liquidador **IVA**, los botones **Créditos** / **Egresos** abren la lista nativa agrupada por categoría (Grouped Tree: No gravada, Gravada, … con facturas debajo). **Saldo** resume totales. En el **2181**, el detalle de facturas está en el smart button **Detalles** y en **Ver facturas** por línea. En **1146**, **Ver agrupado por código DGI**. En la liquidación del mes, **Generar boleto y asientos** queda disponible para usuarios Impuestos UY.

Desde **Liquidación Mensual y Boleto de Pago**, en cada línea del pack usá **Abrir** para ir al liquidador y validarlo. El aviso azul indica el próximo paso. Con la DJ lista, **Generar boleto y asientos** arma las líneas de pago y los asientos. En cada línea cargá el **nº de boleto DGI**, el **PDF del boleto DGI** y, si aplica, el **comprobante bancario**. Sin nº + PDF DGI no se puede **Cerrar / conciliar**.

**TXT para PADI:** en la liquidación del mes (packs **1376, 1146, 1144, 2183**), el botón **TXT DGI (PADI)** prepara los formularios:

| Pack / form | Código TXT | Notas |
|-------------|------------|--------|
| 2181 | `02181` | Se calcula solo |
| 1146 | `01146` | Cuenta IRPF + **Código impuesto 1146** en el tax del asiento |
| 2183 | `02183` | Taxes con **Código impuesto 2183** |
| 1144 | `01144` | Misma cuenta IRPF + **Código impuesto 1144** (CI/NIE/PAS/DNI) |

Si faltan aprobar, abre esos formularios; si ya están aprobados, descarga el `.txt` (o un `.zip`) y lo deja en el chatter. El **1376** y el **1050** no tienen TXT de importación usable desde Odoo: se confeccionan en PADI. El archivo TXT termina en `;` (requisito del instructivo DGI).

**Aprobar / exportar TXT:** hace falta el grupo **Impuestos UY / Aprobador** (o administrador contable) — liquidadores, pack, formularios TXT y sincronización de la DJ. El usuario de impuestos puede calcular y armar boleto, pero no aprobar ni exportar PADI.

---

## 2181 y 1146

Misma pantalla, distinto tipo. Entrada preferida: **TXT DGI (PADI)** en la liquidación del mes (también menús Formularios DGI):

- `Contabilidad → Uruguay → Impuestos → Formularios DGI → 2181 — IVA ventas y compras`
- `Contabilidad → Uruguay → Impuestos → Formularios DGI → 1146 — Retenciones IRPF`

![Lista de reportes DGI (2181 / 1146)](img/odoo-reportes-dgi.jpg)

1. **Nuevo** (o abierto desde el pack). Mes, año y compañía.
2. **Modo de exportación:** totales por partner o detalle por factura.
3. **Calcular.** Revisa las líneas (partner, RUT, importe). **Ver detalle** abre las facturas que alimentan esa línea.
4. **Aprobar** (grupo Aprobador).
5. **Exportar TXT** (mismo grupo). El archivo queda en el formulario.

Estados: Borrador → Calculado → Aprobado → Exportado. **Volver a Borrador** si hay que recalcular.

![Formulario 2181: calcular, aprobar y exportar TXT](img/odoo-reporte-2181.jpg)

### Cómo arma el 2181 (reglas DGI)

El código de línea del impuesto (`Línea 2181`) es el punto de partida; el reporte **reclasifica** según el contacto:

| Situación | Línea DGI | Importe |
|-----------|-----------|---------|
| IVA ventas a **contribuyente** (RUT Uruguay válido) | **502** / **503** | IVA |
| Ventas a **no contribuyente** (CI u otro doc.) | **501** | Base imponible (ventas) |
| IVA compras plaza (directo e indirecto, si el tax está mapeado) | **505** / **506** | IVA |
| IVA importación (cuenta de Ajustes del 1376) | **1** | IVA |
| RUT estructuralmente inválido (p. ej. bloque `22…`) o sin identificación | **Exclusiones** | No va al TXT |

- Instructivo GC/CEDE: el **502/503** es IVA ventas **a contribuyentes**; no se detallan consumidores finales ahí.
- La pestaña **Exclusiones** lista lo que PADI rechazaría o no se puede informar; corregí el RUT en la ficha y volvé a calcular.
- **505/506 plaza:** además del campo Línea 2181, entran solos los impuestos de compra con **Tipo IVA compras DJ 1376** directo/indirecto (22 % → 505, 10 % → 506). El 1376 sigue usando ese tipo para el prorrateo.
- Importes de **ventas** (501/502/503) se guardan/exportan en positivo (como la DJ); las NC quedan negativas. PADI admite ambos signos.
- La línea **1** (importación) usa la misma cuenta de IVA importación del bloque DJ 1376 en Ajustes.

El 1146 usa el mismo circuito (sin esas reclasificaciones del 2181).

![Formulario 1146](img/odoo-reporte-1146.jpg)

No se publica el TXT ni el RUT de la compañía.

---

## 1376 — DJ mensual IVA · IRAE · IP · ICOSA

`Contabilidad → Uruguay → Impuestos → Formularios DGI → 1376 — DJ mensual IVA · IRAE · IP · ICOSA`.

Declaración jurada mensual DGI (CEDE/GC): paneles de IVA, anticipos de IRAE, IP e ICOSA. Agrupa varios liquidadores. El **boleto y los asientos de cierre** se arman en **Liquidación del mes** (un solo camino operativo).

1. **Nuevo.** Mes, año, compañía (o trabajar desde liquidadores + liquidación del mes).
2. **Calcular.** Completa IVA ventas, compras deducibles, excedente, anticipos e IRAE.
3. Revisá pestañas **Ventas** y **Compras**. Completá a mano `Retenciones OTT`, `IPAT`, `ICOSA` e **IVA perdido** si aplica (antes de aprobar).
4. **Aprobar.**
5. Ir a **Liquidación Mensual y Boleto de Pago** → **Generar boleto y asientos** → cargar nº DGI + PDF(s) → **Cerrar / conciliar**.

El comprobante de pago bancario se adjunta en la misma línea del boleto (además del PDF DGI).

![Formulario 1376 nuevo (antes de Calcular): bloques IVA, IRAE y anticipos](img/odoo-reporte-1376.jpg)

---

## Véase también

- [Diferencia de cambio](diferencia-cambio.md)
- [Cuentas e impuestos](cuentas.md)
- [Uso](uso.md)
