# Uso — Uruguay

Operación diaria una vez configurada la compañía.

!!! note "Pendiente de capturas"
    Flujo nativo de Odoo: un solo **Imprimir** / **Enviar**. No hay un segundo botón paralelo para el PDF fiscal.

## Factura de cliente

1. `Contabilidad → Clientes → Facturas` → crear.
2. Partner con RUT válido, diario de ventas, líneas e impuestos.
3. Confirmar. La localización numera y arma el CFE según el diario y el tipo de documento.
4. **Imprimir** usa el PDF del CFE cuando el comprobante está emitido.
5. **Enviar** usa el flujo nativo de Odoo (`account.move.send` / plantilla de correo), no un wizard paralelo.

## Nota de crédito

Desde la factura: crédito nativo de Odoo. El CFE de nota referencia el comprobante original.

## Factura de proveedor

Registro contable del CFE recibido (número, serie, tipo). La conciliación con el listado DGI es un paso aparte.

## Conciliación DGI

`Contabilidad` → herramientas de conciliación CFE de la localización: cruzar lo emitido/recibido en Odoo contra el listado DGI.

Buscar por RUT, número/serie, fecha de factura y fecha de listado; incluir posted y borrador.

## Reportes DGI

Los reportes de detalle leen líneas de impuesto / cuentas. El filtro de diarios, si existe, es opcional (vacío = todos).
