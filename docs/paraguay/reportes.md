# Reportes DNIT

Módulo `l10n_py_tax_reports`. Wizards **por compañía**: no mezclan saldos entre empresas.

`Contabilidad → Paraguay → Reportes DNIT` (RG90, Form 120, EEFF) y **Retención IVA (Variante A)**.

![Menú Paraguay: RG90, Form 120, EEFF, SIFEN](img/odoo-menu-paraguay.jpg)

---

## RG90

`Contabilidad → Paraguay → RG90`.

1. Compañía (fiscal Paraguay).
2. Fecha desde / hasta.
3. Obligación mensual (9550) u otra que use esa empresa.
4. Incluir compras y/o ventas.
5. **Exportar RG90.** El archivo queda en el wizard.

Los tipos DNIT activos de la compañía alimentan el combo de comprobantes papel. Ver [Cuentas](cuentas.md).

![Wizard RG90](img/odoo-rg90.jpg)

No se publica el archivo ni el RUC.

---

## Formulario 120 (IVA)

`Contabilidad → Paraguay → Formulario 120 (IVA)`.

1. Compañía, fecha desde / hasta.
2. **Calcular.** Arma bases e IVA 10 / 5 / exento de ventas y compras, y el saldo (débito − crédito).
3. Revisá los tres bloques.
4. **Exportar PDF** si hace falta presentar o archivar.

Lee los impuestos del plan (IVA 10 / 5 / exento). Si el tax de la factura está mal, el 120 miente.

![Wizard Formulario 120](img/odoo-form120.jpg)

---

## Estados financieros (Form 500)

`Contabilidad → Paraguay → Estados Financieros (Form 500)`.

Usa el código DNIT de cada cuenta (`l10n_py_dnit_code`). Si está vacío, el reporte no cierra.

1. Compañía, rango de fechas, tipo de reporte.
2. **Calcular.** Lista código DNIT, tipo de cuenta y saldo.
3. **Exportar XLSX.**

![Wizard Estados Financieros (Form 500)](img/odoo-eeff.jpg)

---

## Retención IVA (Variante A)

Solo si **esa** empresa usa el circuito. Primero: `Contabilidad → Configuración → Ajustes` → bloque *Paraguay — Retención IVA* (activar Variante A, %, flags de crédito / IRE, diario y cuentas).

Uso: `Contabilidad → Paraguay → Retención IVA (Variante A)`.

1. Compañía, proveedor, fecha.
2. Importe de factura. Si **Aplicar retención** está apagado, no genera asientos.
3. Base, %, diario y cuenta banco.
4. **Crear asientos.** Quedan el pago y, si corresponde, el crédito.

![Wizard Retención IVA Variante A](img/odoo-retencion-iva.jpg)

---

## Véase también

- [Tipo de cambio y diferencia](tipo-cambio.md)
- [Cuentas e impuestos](cuentas.md)
- [Compras](compras.md)
