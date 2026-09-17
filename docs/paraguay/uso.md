# Uso — Paraguay

Operación diaria con SIFEN ya configurado en test.

!!! note "Pendiente de capturas"
    Un solo **Imprimir** / **Enviar**. El PDF default es el KuDE cuando el DE está aprobado. No hay botón paralelo “KuDE”.

## Factura de cliente (DE emitido)

1. `Contabilidad → Clientes → Facturas` → crear.
2. Partner con RUC, diario, condición de venta, presencia, líneas e IVA.
3. En borrador se cargan tipo de DE, timbrado, establecimiento y punto.
4. Confirmar: se transmite a SIFEN (test). Los datos SIFEN del comprobante quedan de solo lectura.
5. Con el DE aprobado, **Imprimir** genera el KuDE (PDF con QR). **Enviar** adjunta KuDE/XML según la plantilla de la compañía.

## Nota de crédito / débito

Documento asociado al DE original. Mismo circuito de envío a SIFEN.

## Factura de proveedor en papel

En `in_invoice`, pestaña SIFEN, grupo de comprobante recibido en papel:

1. Tipo de comprobante.
2. Timbrado del proveedor.
3. Establecimiento (3 dígitos).
4. Punto de expedición (3 dígitos).
5. Número (7 dígitos).

Odoo **no** transmite a SIFEN una factura recibida en papel. Es registro contable (RG90).

## DE recibidos (XML)

`Contabilidad → Proveedores → DE recibidos`: subir XML, procesar, crear la factura proveedor en borrador. Completar cuentas/analítica y confirmar.

## Consulta de RUC

Herramienta de la localización para validar el RUC del partner (padrón / servicio de consulta), sin pegar padrones de un cliente en este sitio.
