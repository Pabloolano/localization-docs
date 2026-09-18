# Uruguay

Localización fiscal Uruguay sobre Odoo 19: **CFE** ante DGI, impuestos, diarios y conciliación.

<div class="grid cards" markdown>

-   **[Configuración](configuracion.md)**

    ---

    Compañía, CFE, sucursales y puntos de emisión.

-   **[Cuentas, diarios e impuestos](cuentas.md)**

    ---

    Plan de cuentas, diarios CFE e IVA.

-   **[Uso](uso.md)**

    ---

    Emitir, imprimir, enviar, e-Remito 181 y e-Resguardo 182.

-   **[Conciliación DGI](conciliacion.md)**

    ---

    Cruzar Odoo contra el listado DGI.

-   **[Reportes DGI](reportes.md)**

    ---

    Formularios 2181, 1146 y 1376.

-   **[Diferencia de cambio](diferencia-cambio.md)**

    ---

    Gravada IVA y revalúos IRAE.

</div>

## Qué cubre esta localización

| Tema | Módulo (orientativo) |
|------|----------------------|
| Núcleo CFE, tipos DGI, diarios | `l10n_uy_einvoice_base` |
| Conector homologado (transporte XML/PDF) | p. ej. `l10n_uy_einvoice_proinfo` |
| Representación impresa | `l10n_uy_einvoice_document` |
| Consulta RUT | `l10n_uy_vat_query` |
| Conciliación vs listado DGI | `l10n_uy_einvoice_conciliation` |
| Reportes DGI (detalle / liquidación) | `l10n_uy_tax_reports` |
| Diferencia de cambio | `l10n_uy_exchange_difference` |

No sustituye el [manual nativo de Accounting](https://www.odoo.com/documentation/19.0/applications/finance/accounting.html): solo lo que agrega la localización.

!!! warning "Testing"
    Hasta validar el circuito, **Modalidad de conexión = Testing**. No uses URLs ni credenciales de producción en un entorno de desarrollo.

!!! note "Capturas"
    Fotos de Odoo 19. Se tapó la compañía, el RUT y menús o diarios propios del cliente. Proveedores y montos se dejan.
