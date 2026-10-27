# Despachante de aduana

Módulo `customs_broker`, repo `custom_broker`. App **Despachante**.

Sirve para cualquier despachante. No envía el trámite a la aduana: la liquidación se anota a mano.

---

## Carpeta y despacho

`Despachante → Carpetas → Nuevo`. El número que aparece es el **correlativo**. Al oficializar se carga el **número oficial** en esa misma carpeta. Una salida es otra carpeta.

1. Estado **Cotización**. En la pestaña Cotización van el tributo estimado, los gastos y el honorario.
2. **Documentos.** Una fila por documento, con su imagen. El RADE se ve solo si la compañía es de Uruguay.
3. Catálogo del cliente: nombre, descripción y NCM. **Armar ítems** exige la factura adjunta y arma las líneas agrupadas por NCM.
4. **Pasar a provisorio** pide la referencia y la liquidación, en el despacho de esa carpeta.
5. **Pedir fondos**, después **Oficializar** con el número de aduana.
6. Canal y fecha de levante, en el despacho. **Registrar levante**.
7. Pestaña **Stock**: depósito, número de stock, manifiesto, contenedor y precinto. El contenedor tiene que cerrar el dígito. La salida indica la carpeta de ingreso y la cantidad que saca.

**Cerrar sin despacho** deja el correlativo ocupado. No pide levante.

El despacho (carátula, ítems, canal, provisorio) se abre con el botón **Despachos**. Hay uno por carpeta.

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

---

## Canal y cierres

En el despacho:

- **Canal:** verde, naranja o rojo.
- **Levante:** la fecha en que la mercadería salió del control.
- **Cierre operativo.** Exige el levante. Si la carpeta abrió stock, el saldo tiene que estar en cero y cada salida en cierre operativo. No factura.
- **Cierre administrativo.** Exige el cierre operativo, el saldo financiado en cero y la factura de honorarios publicada. Si hay salidas, cada una tiene que estar cerrada en lo administrativo. No vuelve a pedir el levante.

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
