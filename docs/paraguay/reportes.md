# Reportes DNIT

Módulo `l10n_py_tax_reports`. RG90, Form 120 y EEFF son **documentos persistentes**
(lista + estados, un registro por período). No mezclan saldos entre empresas.

`Contabilidad → Paraguay → Reportes DNIT` (RG90, Form 120, Form 500, EEFF) y **Retención IVA (Variante A)**.

![Menú Paraguay: RG90, Form 120, EEFF, SIFEN](img/odoo-menu-paraguay.jpg)

---

## RG90

`Contabilidad → Paraguay → Reportes DNIT → RG90`.

1. **Nuevo.** Obligación **Mensual (955)** o **Anual (956)**.
2. **Calcular** → **Aprobar**.
3. **Exportar ZIP** para Marangatu. El ZIP queda en el registro (`RG90/…`).

Los comprobantes **electrónicos SIFEN no entran** en ese CSV: solo papel / RG90. Tipos DNIT activos: [Cuentas](cuentas.md).

![RG90](img/odoo-rg90.jpg)

No se publica el archivo ni el RUC.

---

## Formulario 120 (IVA)

`Contabilidad → Paraguay → Reportes DNIT → Formulario 120 (IVA)`.

1. **Nuevo** del mes. Aperturas 46/51/215 solo la primera vez.
2. **Calcular.** Arma bases e IVA 10 / 5 / exento de ventas y compras.
3. **Aprobar.** Queda en la lista (`F120/…`).
4. **Exportar XLSX** para tipear casillas en Marangatu. El PDF es apoyo interno.

La DJ oficial se carga en Marangatu a mano. Si el tax de la factura está mal, el 120 miente.

![Formulario 120](img/odoo-form120.jpg)

---

## Estados financieros (RG 49/14)

`Contabilidad → Paraguay → Reportes DNIT → Estados Financieros (RG 49/14)`.

Papel de trabajo de Anexos 1 y 2 (Balance y Resultados). **No** es la DJ Form. 500
(casillas web en Marangatu).

Usa el código DNIT de cada cuenta (`l10n_py_dnit_code` en [Cuentas](cuentas.md)).
Si falta, el cálculo se corta. Las cuentas hijas se **suman al padre oficial**
(el planilla DNIT tiene menos filas que el plan NIC).

1. **Nuevo** del ejercicio (1/1–31/12). Tipo: Balance, Resultados o ambos.
2. **Calcular** → **Aprobar.** Queda en la lista (`EEFF/…`).
3. **Exportar XLSX (EF)** → `{RUC}EF.xlsx` (Anexos 1–6, X1 / X1-1).
   Si Marangatu pide `.xls` o `.ods`, convertí ese archivo. El PDF es apoyo.
   Las hojas 3–6 son papel de trabajo; no clonan la planilla oficial.

---

## Formulario 500 (IRE General)

`Contabilidad → Paraguay → Reportes DNIT → Formulario 500 (IRE)`.

Papel de casillas de la DJ de renta (obligación 700). **No** se sube a Marangatu:
se tipea. Reusa el EEFF del mismo ejercicio si ya está calculado.

1. **Nuevo** del ejercicio → **Calcular**.
2. Volvé a Borrador para cargar casillas manuales (pérdidas, créditos, anticipos).
3. **Calcular** de nuevo → **Aprobar** → **Exportar XLSX**.

![Estados Financieros](img/odoo-eeff.jpg)

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
