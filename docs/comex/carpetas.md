# Carpetas COMEX

Módulo `comex`. Una carpeta = una operación de **importación** o **exportación**.

`COMEX → Carpetas`.

![Lista de carpetas](img/odoo-carpetas.jpg)

---

## Crear y avanzar

Lo habitual: desde la OC (importación), la OV (exportación) o una factura de gasto LC → **Generar carpeta COMEX** (crear nueva o unirse a una existente). También `COMEX → Carpetas` → **Nuevo**.

1. Tipo importación o exportación, descripción, países, fechas estimadas.
2. DUA con la máscara del país (`COMEX → Configuración → DUA por país`).
3. **Confirmar** (grupo **Administración COMEX**).
4. **En tránsito.**
5. Importación: **Recibido**. Exportación: **Entregado**.
6. Pestaña **Prorrateo**: se puede armar **antes** de recibir mercadería y con facturas de gasto **en borrador**. La cantidad de la grilla es la comprada (OC/OV). **Dif.** de cada costo capitalizable tiene que quedar en 0.
7. **Cerrar** (importación en Recibido): todas las facturas de la carpeta tienen que estar **posteadas** o canceladas; el prorrateo se rebasea a lo **realmente recibido**; recién ahí se genera el asiento de costo en destino (cuenta puente de Ajustes).
8. **Cancelar** solo en borrador o confirmado.

Estados importación: Borrador → Confirmado → En tránsito → Recibido → Cerrado.  
Estados exportación: … → Entregado → Cerrado.

![Ficha de carpeta: tipo, DUA y estados](img/odoo-carpeta-form.jpg)

---

## Qué se engancha

Una factura de proveedor con costo en destino no se postea sin carpeta (o el check **No pertenece a operación COMEX**).

`COMEX → Facturas sin carpeta` (admin): el pendiente a enganchar. Smart buttons: OC, OV, facturas, recepciones, costo en destino.

Pestaña **Prorrateo**: matriz producto × costo. La columna **Valor FOB** es mercadería; **Costo en Origen** (y otros gastos) van en columnas LC aparte. Mientras la carpeta está abierta usa **cantidad comprada** y suma facturas en borrador (para ver cuánto hay que desembolsar). El **costo en destino** nativo no se crea hasta el cierre, contra lo posteado y lo recibido.

Los productos de gasto LC tienen que facturarse **sobre cantidades pedidas**, no al recibir. Si no, la línea entra en 0 y la grilla muestra Facturado 0. Odoo avisa al postear o vincular esa factura.

Ahí también:

- **Faltante en recepción:** pérdida o backorder, según la compañía.
- **Cuenta puente LC COMEX:** crédito del asiento al cerrar.

![Ajustes COMEX en Inventario](img/odoo-comex-ajustes.jpg)

Al cerrar, si el período contable está cerrado, Odoo avisa (wizard). Factura duplicada en la misma carpeta: aviso, no se silencia.

No copies la cuenta puente ni el DUA de otra empresa.
