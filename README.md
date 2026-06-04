# Liquidador DIAN 🧾

Herramienta web (un solo archivo HTML) que separa y liquida el reporte de
**documentos electrónicos de la DIAN** en segundos. Pensada para que **cualquier
persona del equipo contable** la use: se abre con doble clic, funciona **100%
offline** y nada se sube a internet.

## ¿Qué hace?

A partir del reporte que entrega la DIAN (un `.zip` con un Excel adentro, lleno de
facturas, notas crédito, documentos soporte, nómina y miles de líneas de
*Application response*), el liquidador:

- **Separa** ventas, compras y nómina electrónica.
- **Lleva los documentos soporte a compras**, donde contablemente corresponden.
- **Calcula el subtotal** restando los impuestos al total (`Subtotal = Total − impuestos`).
- **Netea las notas crédito** contra las facturas del mismo proveedor para mostrar la cifra real.
- **Descarta** las líneas de *Application response* que no sirven para la contabilidad.
- **Exporta a Excel** con 5 hojas: `RESUMEN`, `VENTAS`, `COMPRAS`, `NETO x PROVEEDOR` y `NOMINA`.

## Uso

1. Abre `liquidador-dian.html` con doble clic (cualquier navegador, sin internet).
2. Arrastra el `.zip` de la DIAN (o el `.xlsx` ya descomprimido).
3. Revisa los totales en pantalla y descarga el **Excel liquidado**.

## Lógica de clasificación

| Tipo de documento | Destino |
|---|---|
| Application response | Descartar |
| Nomina Individual | Nómina |
| Documento soporte | Compras |
| Nota de crédito | Compras (recibida) / Ventas (emitida), en negativo |
| Factura / Doc. equivalente recibido (Grupo = Recibido) | Compras |
| Factura emitida (Grupo = Emitido) | Ventas |

## Detalles técnicos

- Archivo único autocontenido (~1 MB). Incrusta **SheetJS** (lectura/escritura de
  Excel) y **JSZip** (extracción del `.xlsx` dentro del `.zip`). No requiere instalación
  ni conexión.
- Todo el procesamiento ocurre en el navegador del usuario; los datos nunca salen del equipo.

## Ramas

- `main`: versión estable.
- `dev`: desarrollo de futuras mejoras.

---
🤖 Generado con [Claude Code](https://claude.com/claude-code)
