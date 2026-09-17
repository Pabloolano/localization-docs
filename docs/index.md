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

</div>

## Cómo leer estas guías

Cada país tiene dos bloques, como en el manual de Odoo Accounting:

1. **Configuración** — primera vez por compañía (país fiscal, cuentas, diarios, impuestos, facturación electrónica).
2. **Uso** — el día a día (emitir, imprimir, enviar, conciliar).

Los menús se escriben como en Odoo: `Contabilidad → Configuración → Ajustes`.

!!! warning "Ambiente de prueba"
    En local, CFE y SIFEN se usan en **testing / test**. No apuntar Web Services de producción desde un entorno de desarrollo.

!!! note "Contenido en construcción"
    El sitio y la navegación ya están. Los pasos con captura se cargan a continuación, país por país.

## Qué no va aquí

- RUT, RUC, certificados, claves, CSC, CAE o timbrados reales
- Nombres, cuentas o diarios de un cliente
- Capturas de una base de producción
- Personalizaciones de un solo cliente (Handy, COMEX, etc.)
