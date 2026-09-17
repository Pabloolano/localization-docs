# Cuentas, diarios e impuestos — Paraguay

Instalá el chart **genérico** de la localización (`l10n_py`). No copies el plan de otra base ni de otra compañía de la misma base.

---

## Plan de cuentas

1. Compañía activa, país fiscal Paraguay.
2. Instalar `l10n_py` (chart `py_generico`).
3. `Contabilidad → Configuración → Plan de cuentas`.

    ![Plan de cuentas Paraguay (códigos DNIT / Form 500)](img/odoo-plan-cuentas.jpg)

4. Revisar clientes, proveedores, IVA, bancos, IRE / diferencia de cambio.

Códigos DNIT en cuentas (`l10n_py_dnit_code`) alimentan EEFF. Si están vacíos, el reporte legal no cierra.

Cada wizard fiscal pide **compañía**: no mezcla saldos entre empresas.

---

## Diarios

`Contabilidad → Configuración → Diarios`.

![Diarios de la compañía Paraguay: ventas SIFEN, compras, banco, varios](img/odoo-diarios.jpg)

| Tipo | Rol PY |
|------|--------|
| Ventas | Emite DE si FE está activa. Timbrado / est / punto salen de la compañía; el diario no “es” el timbrado. |
| Compras | Factura papel (RG90) o borrador creado desde DE recibido. |
| Banco / caja | Pagos nativos. |
| Varios | Ajustes, retención IVA (si usa Variante A), diferencia de cambio. |

No reutilices diarios de una empresa Uruguay ni de otra PY.

---

## Impuestos IVA

`Contabilidad → Configuración → Impuestos`.

![Impuestos IVA 10 / 5 / exento del plan Paraguay](img/odoo-impuestos.jpg)

Tasas del plan genérico:

- IVA 10 %
- IVA 5 %
- Exento

Cuentas de débito/crédito = las de **esta** compañía. En la línea de factura, el tax es el que viaja al DE y al Form 120.

---

El menú **Paraguay** agrupa reportes DNIT, masters SIFEN y DE recibidos:

![Menú Paraguay: RG90, Form 120, EEFF, SIFEN, DE recibidos](img/odoo-menu-paraguay.jpg)

## Tipos DNIT (papel / RG90)

Catálogo global + **cuáles están activos en esta compañía** (pestaña de tipos DNIT).

![Tipos de comprobante DNIT activos (papel / RG90)](img/odoo-tipos-dnit.jpg)

Sirven para el combo de comprobante en facturas **papel**. Con FE activa, la factura de **cliente** electrónica no usa ese combo: el tipo de DE vive en SIFEN.

Exportación: `Contabilidad → Paraguay → RG90`.

![Wizard RG90: rango, compras/ventas y obligación mensual](img/odoo-rg90.jpg)

---

## Retención IVA (Variante A)

Si esa empresa usa el circuito:

1. `Contabilidad → Configuración → Ajustes` → bloque *Paraguay — Retención IVA*.
2. Activar Variante A, % default, flags de crédito / IRE.
3. Mapear cuentas + diario (o sugerir desde códigos del plan).

Uso: `Contabilidad → Informes → Impuestos → Retención IVA (Variante A)`. Si “Aplicar retención” está apagado, no genera asientos.

---

## Tipo de cambio DNIT

Módulo `l10n_py_currency_rate`: cotizaciones por compañía. No compartir TC “a mano” entre empresas.

---

## Véase también

- [Configuración SIFEN](configuracion.md)
- [Uso](uso.md)
