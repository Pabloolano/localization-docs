# Configuración — Uruguay

Primera vez por compañía. Orden recomendado (igual que un [Get started](https://www.odoo.com/documentation/19.0/applications/finance/accounting.html) de Odoo: setear antes de operar).

!!! note "Pendiente de capturas"
    Texto de estructura. Las capturas salen de una compañía **demo**, nunca de un cliente.

## 1. Compañía

1. `Ajustes → Empresas` → abrir la compañía.
2. País fiscal **Uruguay**.
3. Moneda de la compañía.
4. RUT en el campo nativo `vat` (en demo: placeholder, no un RUT real).
5. Dirección y datos de contacto que van al CFE.

## 2. Plan de cuentas y diarios

1. Instalar / verificar el plan Uruguay de la localización (no copiar el de otra empresa).
2. `Contabilidad → Configuración → Diarios`: ventas, compras, banco, caja, misceláneo.
3. Cada diario con la secuencia y el tipo de documento CFE que le corresponde.

## 3. Impuestos

1. `Contabilidad → Configuración → Impuestos`.
2. IVA y percepciones/retenciones que use la compañía.
3. Cuentas de impuesto coherentes con el plan.

## 4. Facturación electrónica (CFE)

1. En la compañía: modo **testing** hasta validar el circuito.
2. Datos del emisor y del conector (ambiente de prueba).
3. CAE / rangos según el tipo de CFE — valores de demo o de DGI test, no de producción de un cliente.

!!! warning
    No pegar certificados, tokens ni CAE reales en este manual ni en el repositorio.

## 5. Tipos de documento

`Contabilidad → Configuración → Tipos de documento` (Latam): e-Factura, e-Ticket, notas de crédito/débito, etc., activos para esa compañía.

## 6. Prueba

Antes de producción: un CFE de venta en testing, imprimir el PDF default y revisar el estado ante DGI.
