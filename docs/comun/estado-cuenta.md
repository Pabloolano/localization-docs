# Estado de cuenta del contacto

Módulo `account_partner_statement` (localization-common).

Cuenta corriente por **moneda del comprobante**, separando lado Cliente y Proveedor.

---

## Dónde está

- Menú **Contabilidad → Informes → Partners → Estado de Cuenta del Contacto**
- En la ficha del contacto: botón **Estado de cuenta**

---

## Uso

1. Elegí partner, compañía, lado (Cliente / Proveedor) y rango de fechas.
2. **Actualizar** arma el listado (saldo inicial + movimientos del período).
3. **PDF** / **Excel** / **Enviar por mail** usan el mismo contenido.

Columnas:

| Columna | Contenido |
|--------|-----------|
| Fecha | Fecha del comprobante |
| Concepto | Factura o pago (enlace al documento) |
| Comprobantes | En filas de **pago**: facturas o bills conciliados (nativo). Varios en la misma celda, separados por coma; en pantalla cada uno es enlace |
| Debe / Haber / Saldo | Importes en la moneda del movimiento |

El PDF usa el **layout de reporte de la compañía** (logo, dirección y pie nativos). No hay un segundo logo en el cuerpo del informe.

---

## Notas

- **Incluir facturas de canje** mezcla el otro lado (cliente↔proveedor) cuando aplica.
- Pagos sin conciliación dejan **Comprobantes** vacío.
