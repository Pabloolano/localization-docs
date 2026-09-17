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

    Emitir, imprimir, enviar y notas de crédito.

-   **[Conciliación DGI](conciliacion.md)**

    ---

    Cruzar Odoo contra el listado DGI.

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
    Los pasos están escritos. Las fotos salen de una **compañía demo** (sin RUT real). Todavía no están en esta página.
