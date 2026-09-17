# Configuración — Paraguay

Primera vez por compañía. Cada empresa fiscal PY tiene su propia regla: no reutilizar códigos ni secretos de otra.

!!! note "Pendiente de capturas"
    Estructura de seteo. Capturas solo de compañía **demo**.

## 1. Compañía

1. `Ajustes → Empresas` → abrir la compañía.
2. País fiscal **Paraguay**.
3. Moneda (habitualmente PYG).
4. RUC + dígito verificador en los campos de la localización (demo: placeholder).

## 2. Plan de cuentas y diarios

1. Instalar el chart genérico de la localización (`l10n_py`), no copiar el de otra base.
2. Revisar diarios de ventas, compras, banco y caja para esa compañía.
3. Impuestos IVA 10 %, 5 % y exento del plan.

## 3. SIFEN (si emite documentos electrónicos)

En la compañía, pestaña SIFEN:

1. Proveedor SIFEN activo.
2. Ambiente **test** (hasta la ventana de producción, que es una decisión explícita).
3. Certificado de **test** y CSC de **test** (nunca pegar archivos `.p12` ni claves en git).
4. Timbrado, establecimiento y punto de expedición de ambiente de prueba.
5. Actividades económicas requeridas por el DE.

!!! warning
    Test y producción usan certificados y CSC distintos. Este manual no incluye valores reales.

## 4. Tipos de documento DNIT

Activar los tipos que la compañía usa (factura electrónica, nota de crédito, etc.). El papel / RG90 se registra aparte en la factura de proveedor.

## 5. Correo al aprobar el DE

Usar plantilla de correo editable en la compañía (asunto y cuerpo configurables). No hardcodear el texto del mail al cliente.

## 6. Prueba

Un DE de venta en **test**: confirmar, esperar aprobación, **Imprimir** (KuDE) y **Enviar** por el flujo nativo. Un solo camino de PDF.
