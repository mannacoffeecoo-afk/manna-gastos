[README.md](https://github.com/user-attachments/files/32317214/README.md)
# MANNA Gastos de Eventos

App web para organizar en un solo lugar los gastos, recibos, ventas y el resultado
de cada evento o market de **MANNA Coffee & Crepes**.

Pensada para usarse desde el iPhone mientras el evento está pasando: botones grandes,
formularios cortos y la foto del recibo en el momento.

**Abrir la app:** https://mannacoffeecoo-afk.github.io/manna-gastos/

---

## Qué hace

- **Eventos**: nombre, fecha, lugar, notas y estado (en preparación, en curso, cerrado).
  Un evento cerrado se puede reabrir para corregir.
- **Gastos**: importe, concepto, categoría, quién pagó, si fue dinero de MANNA o personal,
  fecha y notas. Cada compra se registra por separado.
- **Recibos**: foto desde la cámara o archivo del teléfono, varios por gasto, se pueden
  añadir después. Se guarda el archivo original.
- **Reembolsos**: quién puso dinero propio, cuánto se le debe y cuánto se le ha devuelto.
  Un reembolso no se cuenta como gasto nuevo.
- **Ventas**: cantidades totales por producto al terminar el evento, con descuentos y
  devoluciones. El precio usado queda congelado en ese evento.
- **Caja**: caja inicial, efectivo contado, propinas, impuestos, cobros con tarjeta y
  comisiones, cada uno por separado.
- **Conciliación**: compara las ventas por producto con lo realmente cobrado y muestra la
  diferencia. No ajusta los números por su cuenta.
- **Respaldo**: exporta un ZIP con todo, incluidos los recibos originales, y lo restaura.

## Cómo instalarla en el iPhone

1. Abre la dirección de arriba **en Safari**. Tiene que ser Safari.
2. Botón **Compartir** → **Añadir a pantalla de inicio**.
3. Ábrela desde ese ícono.

Después de la primera carga funciona sin conexión.

> **No funciona tocando `index.html` en la app Archivos.** Esa vista previa del iPhone
> muestra la página pero no ejecuta JavaScript, y la app se queda en "Abriendo MANNA Gastos".

## Dónde viven los datos

En el navegador del teléfono (IndexedDB), no en este repositorio ni en ningún servidor.
Quien abra la dirección desde otro dispositivo ve una app **vacía**: no hay forma de ver
los gastos, recibos ni números de MANNA desde fuera.

Eso también significa que **si se borran los datos del navegador, se usa navegación privada
o se cambia de teléfono, la información se pierde**. No hay copia automática en iCloud.
Por eso: **exportar un respaldo al cerrar cada evento**, y guardarlo en Archivos, en una
carpeta llamada `Respaldos MANNA Gastos`.

## Reglas de los números

- Todo el dinero se maneja en centavos enteros: sin errores de redondeo acumulados.
- El impuesto y las propinas nunca se cuentan como ganancia.
- Las comisiones de tarjeta se descuentan una sola vez, aunque el importe registrado ya
  venga neto.
- La caja inicial no es venta ni gasto.
- Un gasto pagado con el efectivo del puesto genera la salida de caja, sin contarse dos veces.
- El resultado aparece como **provisional** mientras falten datos del cierre o haya
  diferencias sin aclarar.

Resultado del evento = ventas sin impuesto − costos atribuibles − comisiones de cobro.

## Archivos

| Archivo | Para qué |
|---|---|
| `index.html` | La app completa. Un solo archivo, sin dependencias externas. |
| `sw.js` | Service worker: permite abrir la app sin conexión. |
| `manifest.webmanifest` | Nombre, colores e instalación en pantalla de inicio. |

Los tres tienen que estar en la misma carpeta y conservar sus nombres.

## Si no abre

Mira el texto pequeño debajo de "Abriendo MANNA Gastos":

- **`cargando el programa…`** sin cambiar → JavaScript no se está ejecutando. Estás en una
  vista previa de archivo, no en Safari con una dirección `https://`.
- **`comprobando el navegador…`** o cualquier otra fase → JavaScript sí corre. En unos
  segundos aparece una pantalla explicando el problema, con un botón **Copiar detalles**.

Esa pantalla nunca borra datos ni recibos. También está disponible en **Ajustes → Diagnóstico**
cuando la app sí abre.

## Conviviendo con el cotizador

Si el cotizador de eventos de MANNA está publicado en otro repositorio del mismo usuario,
su service worker sólo cubre su propia carpeta. Por eso esta app va en un repositorio
aparte: así ninguno intercepta las páginas del otro.
