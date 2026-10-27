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
