# Reportes DGI

Módulo `l10n_uy_tax_reports`. Genera el **2181**, el **1146** y la liquidación **1376** de **esta** compañía.

`Contabilidad → Uruguay → Reportes DGI`.

![Menú Uruguay: diferencia de cambio y reportes DGI](img/odoo-menu-uruguay.jpg)

El filtro de diarios en Ajustes es **opcional**: vacío = todos los diarios de la compañía. El 1376 no se “arregla” eligiendo un diario: lee el diseño contable (cuentas e impuestos mapeados). La diferencia de cambio **Gravada (IVA)** alimenta el 2181: corré ese cálculo antes del mes.

---

## Antes de calcular

En `Contabilidad → Configuración → Ajustes` (compañía fiscal Uruguay):

1. **Diarios para Reportes DGI** — filtro opcional.
2. **Cuenta Retención IRPF** — si esa empresa usa IRPF.
3. Bloque **DJ 1376 — Anticipos**: coeficiente y mínimo IRAE, anticipos IPAT / ICOSA, cuentas de importación.

En cada impuesto (`Contabilidad → Configuración → Impuestos`):

| Campo | Para qué |
|-------|----------|
| Línea 2181 | Agrupa el tax en el 2181 |
| Línea 1146 | Agrupa el tax en el 1146 |
| Categoría DJ 1376 (venta) | Clasifica ventas de la liquidación |
| Tipo IVA compras 1376 | Clasifica compras de la liquidación |

Si el tax no está mapeado, el XML CFE puede estar bien y el reporte igual sale incompleto.

---

## 2181 y 1146

Misma pantalla, distinto tipo. Menús:

- `Contabilidad → Uruguay → Reportes DGI → 2181 — IVA ventas y compras`
- `Contabilidad → Uruguay → Reportes DGI → 1146 — Retenciones IRPF`

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

`Contabilidad → Uruguay → Reportes DGI → 1376 — DJ mensual IVA · IRAE · IP · ICOSA`.

Declaración jurada mensual DGI (CEDE/GC): paneles de IVA, anticipos de IRAE, IP e ICOSA. El boleto sale del cuadro resumen y discrimina por impuesto. No exporta TXT en esta pantalla.

1. **Nuevo.** Mes, año, compañía.
2. **Calcular.** Completa IVA ventas, compras deducibles, excedente, anticipos e IRAE.
3. Revisá pestañas **Ventas** y **Compras**.
4. **Aprobar.**

`Retenciones OTT`, `IPAT` e `ICOSA` se pueden completar a mano si el cálculo no los trae.

![Formulario 1376 nuevo (antes de Calcular): bloques IVA, IRAE y anticipos](img/odoo-reporte-1376.jpg)

---

## Véase también

- [Diferencia de cambio](diferencia-cambio.md)
- [Cuentas e impuestos](cuentas.md)
- [Uso](uso.md)
