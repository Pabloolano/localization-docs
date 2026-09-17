# Paraguay

Localización fiscal Paraguay sobre Odoo 19: **SIFEN** (DNIT), plan de cuentas, KuDE y documentos electrónicos recibidos.

<div class="grid cards" markdown>

-   **[Configuración](configuracion.md)**

    ---

    Compañía, SIFEN, timbrado, establecimiento y punto.

-   **[Cuentas, diarios e impuestos](cuentas.md)**

    ---

    Chart genérico, IVA 10/5/exento, RG90.

-   **[Uso](uso.md)**

    ---

    Emitir DE, KuDE, correo, NC.

-   **[Compras](compras.md)**

    ---

    Papel, XML recibido y consulta RUC.

</div>

## Qué cubre esta localización

| Tema | Módulo (orientativo) |
|------|----------------------|
| Plan de cuentas y geo/RUC base | `l10n_py` |
| Masters SIFEN en compañía y factura | `l10n_py_einvoice_base` |
| Conector mTLS / SOAP DNIT | `l10n_py_einvoice_sifen` |
| KuDE + correo al aprobar | `l10n_py_einvoice_document` |
| DE recibidos | `l10n_py_de_received` |
| Consulta RUC | `l10n_py_ruc_query` |
| TC DNIT | `l10n_py_currency_rate` |
| RG90 / Form 120 / EEFF | `l10n_py_tax_reports` |
| Diferencia de cambio | `l10n_py_exchange_difference` |

!!! warning "SIFEN Test"
    En implementación y en local: **Modalidad de conexión = Testing**. No se documenta ni se prueba emisión a producción desde un entorno de desarrollo.

!!! note "Capturas"
    Fotos de Odoo 19. Se tapó la compañía, el RUC, el chatter y los certificados. Clientes y montos se dejan como ejemplo.
