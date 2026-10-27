# Cotizador COMEX

Módulo `comex_quote` (en implementación: el circuito de UI ya está; la IA y el catálogo NCM se siguen afinando).

App **COMEX Cotizador → Cotizaciones**. Catálogo: **Consulta NCM**.

**Cerrar cotización** pregunta si se crea la orden de compra y si se crea la factura de proveedor en borrador. Si no se marca ninguna, la cotización queda histórica y se guarda el NCM de cada línea de mercadería.

![Lista de cotizaciones](img/odoo-cotizaciones.jpg)

---

## Armar un presupuesto

1. **Nuevo.** Adjuntá la factura comercial (PDF o imagen).
2. **Continuar** — wizard de costos (flete, seguro, gastos origen/terminal/línea, flete importación, honorario, despacho). Una línea tipeada, sin PDF, entra por el mismo wizard: guarda los costos y no extrae. Con PDF, **Procesar** extrae las líneas.
3. La IA extrae líneas y sugiere NCM. Si no hay partner: **Crear proveedor**.
4. Revisá confianza, documentos exigidos y alerta de prohibido (rojo).
5. **Reclasificar NCM (IA)** o **Buscar NCM**. **Confirmar al catálogo**. **Crear producto** si no existe.
6. Con el NCM elegido, cada línea de mercadería muestra la **liquidación orientativa**: valor en aduana, arancel, TGA, IMESI, IVA, tasa consular, anticipos y el total. El valor en aduana es la mercadería más la parte de flete, seguro, gastos en origen y flete de importación. El reparto se elige en **Prorrateo de costos** (valor, cantidad, peso o volumen). Si la factura ya trae ese costo como línea, manda la línea; si no, manda la columna del cabezal. Terminal, honorarios y gastos de despacho se ven aparte y no entran en esos tributos.
7. El beneficio es uno solo y arranca en **régimen general** (el arancel de la partida). Si el origen de la mercadería —o, si no está, el país de la factura— es Argentina, Brasil o Paraguay, se puede elegir el **certificado Mercosur**: el arancel queda liberado según el margen DNA. Bolivia, Chile y Venezuela permiten anotar su certificado (ACE 36, ACE 35 o ACE 59) y el arancel no cambia. **Margen ALADI 504** es la otra opción, por país, y no se combina con el certificado. **Liberación** reemplaza a esos dos: en la línea se elige una fila vigente de esa partida (código, porcentajes y fechas; el feed no trae el nombre) y esos porcentajes son exenciones del arancel, la TGA, el IVA y el IMESI. Si las líneas tienen orígenes distintos, la pregunta es por línea. Una factura brasileña de mercadería china no pregunta el certificado. Si la factura está en dólares, se puede usar la tasa DNA en lugar de la tasa de la compañía. En otra moneda se muestra el número DNA y no se convierte.

**Cerrar cotización** hace dos preguntas. La orden de compra lleva las líneas de la factura. Si el incoterm es CIF, entran todas. Con cualquier otro no entran flete ni seguro. El costo sale con el servicio de la guía (Flete, Seguro, Retiro en origen, Gastos locales, Despachante) y conserva la descripción. Si la línea ya es costo en destino, ese producto queda. En Otro hay que elegirlo. La fecha de la orden es el día de la factura. Si hay PDF, se adjunta. La factura de proveedor queda en borrador con las líneas de la factura, no con los tributos estimados ni el prorrateo, y tampoco se publica. Si no se marca ninguna, la cotización queda histórica y el NCM confirmado de cada línea de mercadería entra al catálogo. Crear la orden no enseña el catálogo. El incoterm se copia a la orden y después no se edita en la cotización. Una cotización cancelada o vencida no se cierra por este botón. La barra de estado no pasa a Convertido sola. La carpeta se crea después, desde la orden. El cartel de la cotización sigue siendo una estimación: el despachante confirma el NCM.

![Cotización: archivo, costos y líneas NCM](img/odoo-cotizacion.jpg)

La API key de IA vive en `Ajustes → Inventario → COMEX Cotizador / IA`, **por compañía**. No va a git ni a este sitio.

![Ajustes: proveedor de IA (sin clave)](img/odoo-cotizador-ajustes.jpg)

!!! warning
    La clasificación NCM es asistencia. El despachante confirma la partida. Un NCM prohibido o en conflicto de catálogo se marca en rojo: no lo ignore.
