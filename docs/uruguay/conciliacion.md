# Conciliación DGI — Uruguay

Cruzar lo que está en Odoo con el **listado que baja DGI** (CFE recibidos / emitidos). Sirve para no dar por “falta factura” algo que ya está, o al revés.

!!! warning "Buscar bien antes de crear"
    Un CFE puede estar en Odoo con **otro número** (serie interna vs número DGI), **otra fecha** (fecha de factura vs fecha del listado vs fecha de pago) u **otro tipo** (factura vs NC). Crear un duplicado ensucia IVA y pagos.

---

## Dónde

`Contabilidad → Uruguay → Conciliación CFE DGI`.

1. Cargá / importá el listado DGI del período.
2. El wizard matachea contra `account.move` de la compañía activa.
3. Revisá las líneas: OK, duda, falta en Odoo, falta en DGI.

---

## Cómo buscar un comprobante que “no está”

Antes de concluir que falta:

1. **RUT** del partner, no solo el número DGI.
2. Número cercano, serie (`cfe_serie`), número CFE, `name` de la factura, referencia.
3. Fecha de factura **y** fecha del listado **y** fecha de pago (pueden ser meses distintos).
4. Estados `posted` **y** `draft`.
5. Tipos `in_invoice` e `in_refund` (una NC no es una factura).
6. Descartar cobranza propia, asientos sueltos y resguardos antes de pedir “bajar y crear factura”.

Anotá qué buscaste y por qué no matchea. No crees facturas “para que cierre el Excel” sin ese veredicto.

---

## Qué no es conciliación DGI

- Pagos / extracto bancario (eso es conciliación de banco nativa).
- Reportes 2181/1146 (detalle de impuestos; leen líneas, no el matching DGI).
- El PDF impreso: un CFE puede estar aceptado y el PDF verse después.

---

## Véase también

- [Uso](uso.md)
- [Configuración](configuracion.md)
