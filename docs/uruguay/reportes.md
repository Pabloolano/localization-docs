# Reportes e Impuestos DGI

Módulo `l10n_uy_tax_reports`. Tres usos distintos bajo `Contabilidad → Uruguay → Impuestos`:

| Menú | Para qué |
|------|----------|
| **Liquidación Mensual y Boleto de Pago** | Boleto → asientos de cierre → candado / conciliación |
| **Liquidadores** | Detalle y cálculo de **cada impuesto** habilitado en la compañía |
| **Formularios DGI** | Lo que se presenta a DGI (2181, 1146, 1376, …) según impuestos habilitados |

Los ítems de **Liquidadores** y **Formularios DGI** se muestran según los tildes de **Impuestos UY** en la compañía (p. ej. IVA → liquidador IVA + formularios 2181 y 1376).

El **1376** agrupa varios liquidadores; el detalle del IVA se mira en **Liquidadores → IVA**, no en el boleto.

![Menú Uruguay: diferencia de cambio y reportes DGI](img/odoo-menu-uruguay.jpg)

El filtro de diarios en Ajustes es **opcional**: vacío = todos los diarios de la compañía. El 1376 no se “arregla” eligiendo un diario: lee el diseño contable (cuentas e impuestos mapeados). La diferencia de cambio **Gravada (IVA)** alimenta el 2181: corré ese cálculo antes del mes.

---

## Antes de calcular

En `Contabilidad → Configuración → Ajustes` (compañía fiscal Uruguay), bloque **Impuestos UY** (también pestaña en la ficha de la compañía):

1. Qué impuestos habilitar (IVA, IRAE, IPAT, …).
2. **Diarios para Reportes DGI** — filtro opcional.
3. Cuentas y parámetros de liquidación: diario de cierre, DGI a pagar, IVA/excedente/OTT, anticipos IRAE/IP/ICOSA, IRPF, importación. Sin diario de cierre no se pueden generar asientos desde **Liquidación del mes**.

En cada impuesto (`Contabilidad → Configuración → Impuestos`):

| Campo | Para qué |
|-------|----------|
| Línea 2181 | Agrupa el tax en el 2181 |
| Línea 1146 | Agrupa el tax en el 1146 |
| Categoría DJ 1376 (venta) | Clasifica ventas de la liquidación |
| Tipo IVA compras 1376 | Clasifica compras de la liquidación |

Si el tax no está mapeado, el XML CFE puede estar bien y el reporte igual sale incompleto.

---

## Liquidadores (detalle por impuesto)

`Contabilidad → Uruguay → Impuestos → Liquidadores → …`

Ahí se calcula y aprueba cada impuesto del mes (montos a pagar / crédito). Es el lugar del **detalle de liquidación** (p. ej. IVA), no el armado del boleto.

En el liquidador **IVA**, los botones **Créditos** / **Egresos** abren la lista nativa agrupada por categoría (Grouped Tree: No gravada, Gravada, … con facturas debajo). **Saldo** resume totales. En **2181 / 1146**, **Ver agrupado por código DGI**. En la liquidación del mes, **Generar boleto y asientos** queda disponible para usuarios Impuestos UY.

Desde **Liquidación Mensual y Boleto de Pago**, en cada línea del pack usá **Abrir** para ir al liquidador y validarlo. El aviso azul indica el próximo paso. Con la DJ lista, **Generar boleto y asientos** arma las líneas de pago y los asientos. En cada línea cargá el **nº de boleto DGI**, el **PDF del boleto DGI** y, si aplica, el **comprobante bancario**. Sin nº + PDF DGI no se puede **Cerrar / conciliar**.

**TXT para PADI:** en la liquidación del mes (pack 1376 o 1146), el botón **TXT DGI (PADI)** calcula los formularios del período (2181 y, si está habilitado, 1146). Si faltan aprobar, abre esos formularios; si ya están aprobados, descarga el `.txt` (o un `.zip` si hay más de uno) y lo deja en el chatter. El **1376** no tiene TXT de importación desde Odoo: se confecciona en PADI.

---

## 2181 y 1146

Misma pantalla, distinto tipo. Menús (también alcanzables desde **TXT DGI (PADI)** en la liquidación del mes):

- `Contabilidad → Uruguay → Impuestos → Formularios DGI → 2181 — IVA ventas y compras`
- `Contabilidad → Uruguay → Impuestos → Formularios DGI → 1146 — Retenciones IRPF`

![Lista de reportes DGI (2181 / 1146)](img/odoo-reportes-dgi.jpg)

1. **Nuevo**. Mes, año y compañía.
2. **Modo de exportación:** totales por partner o detalle por factura.
3. **Calcular.** Revisa las líneas (partner, RUT, importe). **Ver detalle** abre las facturas que alimentan esa línea.
4. **Aprobar.**
5. **Exportar TXT.** El archivo queda en el formulario.

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
