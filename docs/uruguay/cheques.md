# Cheques — Uruguay

Módulo `l10n_uy_check`. Cheques **propios** y de **terceros**. Un cheque se
da por pagado o cobrado **cuando el extracto bancario lo confirma**. El
módulo no inventa el movimiento contra el banco.

`Contabilidad → Cheques`.

---

## Configuración

`Ajustes → Contabilidad`, bloque *Gestión de Cheques Uruguay*:

- Cuentas **Cheques diferidos** / **en cartera** (UYU y USD)
- Mail de alertas, días de tolerancia y de aviso de vigencia

Los métodos **Cheques Propios**, **Cheques Terceros Nuevos** y **Cheques de
Terceros (en cartera)** no se agregan solos: habilitalos en el diario de
banco (propios) o en un diario de **Efectivo** de cartera (terceros).

Chequeras: `Contabilidad → Cheques → Chequeras` (o Configuración → Cheques).

---

## Cheques propios

`Contabilidad → Cheques → Cheques Propios`.

1. Pagá al proveedor con el método **Cheques Propios** (al día o diferido).
2. El asiento usa la cuenta puente de diferidos si aplica.
3. Cuando el banco lo debita, conciliá el extracto: ahí se confirma.

**Anular** solo si todavía no lo debitó el banco.

Informe: `Contabilidad → Cheques → Informes → Provisión de Cheques Propios`.

---

## Cheques de terceros

`Contabilidad → Cheques → Cheques de Terceros`.

1. Cobrá al cliente con **Cheques Terceros Nuevos** (quedan en cartera).
2. **Depositar** (uno o varios) al banco.
3. O **endosar** a un proveedor (método *en cartera*).
4. **Rechazar** / **Devolver** reabren la deuda del tercero.

Un diferimiento mayor a 180 días **avisa**, no bloquea.

Informe: `Contabilidad → Cheques → Informes → Cartera de Cheques de Terceros`.

Los avisos (propios sin debitar, a depositar, vigencia, chequera por
agotarse) salen por mail HTML; la imagen del cheque, si hay, va al chatter.

---

## Véase también

- [Uso](uso.md)
- [Pagos](../comun/pagos.md)
