# Localizaciones Odoo 19

Guías de **configuración** y **uso** de las localizaciones fiscales Uruguay y Paraguay, al estilo de la [documentación de usuario de Odoo](https://www.odoo.com/documentation/19.0/).

Odoo 19 Enterprise. Textos genéricos: compañía demo, placeholders, sin datos de un cliente puntual.

<div class="grid cards" markdown>

-   **Uruguay**

    ---

    CFE (DGI), diarios, impuestos y conciliación.

    [Abrir Uruguay](uruguay/index.md)

-   **Paraguay**

    ---

    SIFEN (DNIT), plan de cuentas, KuDE y DE recibidos.

    [Abrir Paraguay](paraguay/index.md)

-   **Común**

    ---

    Analítica, captcha, pagos, segunda moneda y color de barra.

    [Abrir común](comun/index.md)

-   **COMEX**

    ---

    Carpetas de importación/exportación y cotizador.

    [Abrir COMEX](comex/index.md)

</div>

## Cómo leer estas guías

Cada país, como en el manual de Odoo Accounting:

1. **Configuración** — compañía, CFE/SIFEN, cuentas, diarios, impuestos.
2. **Uso** — emitir, imprimir, enviar, conciliar / compras.

Los menús se escriben como en Odoo: `Contabilidad → Configuración → Ajustes`.

!!! warning "Ambiente de prueba"
    En local, CFE y SIFEN se usan en **testing / test**. No apuntar Web Services de producción desde un entorno de desarrollo.

!!! note "Capturas"
    Fotos de Odoo 19 sobre una base real. Se tapó nombre de **compañía**, RUT/RUC, chatter, certificados y menús o diarios propios de un cliente. Proveedores y montos se dejan como ejemplo.

## Qué no va aquí

- RUT, RUC, certificados, claves, CSC, CAE, timbrados o CDC reales
- Nombres, cuentas o diarios de un cliente
- Cavas, Handy y cualquier menú de un solo cliente
- `l10n_uy_gov_reference` (todavía verde)
- Onboarding de empresa (descartado)
