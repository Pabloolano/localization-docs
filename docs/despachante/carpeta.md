# Despachante de aduana

Módulo `customs_broker`, repo `custom_broker`. App **Despachante**.

Sirve para cualquier despachante. No envía el trámite a la aduana: la liquidación se anota a mano.

---

## Carpeta y despacho

`Despachante → Despachos → Nuevo`.

1. Cliente y tipo: importación, exportación o tránsito.
2. Carátula: destinación, aduana, incoterm, documento de transporte y factura comercial.
3. Provisorio: referencia, fecha, cotización de la aduana del día y liquidación.
4. Ítems: descripción, NCM, cantidad, unidad, origen, peso y valor.

Al guardar, Odoo abre la carpeta y un despacho. En la carpeta, **Nuevo despacho** abre otro de la misma carpeta. El botón **Despachos** abre el formulario si hay uno, y la lista si hay más. `Despachante → Carpetas` muestra esa carpeta. Los archivos van en el chatter. La numeración es de cada compañía.

En un despacho que no es el primero de la carpeta, cada ítem tiene que tener **Ítem de origen**: una línea de otro despacho de la misma carpeta. La cantidad y el peso no pueden pasar el saldo. El NCM tiene que ser el mismo.

---

## Fondos

En la compañía, grupo Despachante:

- **Fondos de terceros:** pasivo corriente.
- **Adelantos por cuenta de clientes:** activo.
- **Cuenta de anticipo:** la de Ventas. Tiene que ser un pasivo corriente. Ahí va el anticipo de honorarios, no el tributo.

En la carpeta:

1. **Honorarios** abre un pedido de venta de esa carpeta. Si ese pedido está cancelado, abre uno nuevo. Las líneas quedan en la cuenta analítica de la carpeta, en el plan Despachante. El anticipo y la factura son los botones del pedido. El interés, si se cobra, es otra línea con el importe que cargue el usuario.
2. **Fondos de terceros** abre un cobro del cliente. No es una factura.
3. **Pago a la aduana** abre un pago de proveedor. El contacto de la aduana se elige en ese pago.

**Saldo financiado** es lo adelantado a la aduana menos lo cobrado de terceros. La deuda del honorario no entra en ese saldo.

El aviso del formulario lo dice: nada de esto sale hacia la aduana.

---

## NCM

En la compañía, **Dígitos del NCM** (grupo Despachante). Paraguay: 8. Uruguay: 10. Si queda vacío, Odoo usa 8.

El código se guarda sin puntos. Si el largo no coincide, Odoo no deja grabar la línea.

---

## Configuración

`Despachante → Configuración`.

- **Destinaciones.** Paraguay trae las de uso diario (IC04, EC01, IDA3 y las de esa lista). Se pueden agregar.
- **Aduanas.** Se cargan a mano, con país.

La destinación y la aduana tienen que ser del mismo país que la compañía, y la destinación del mismo tipo que la carpeta.
