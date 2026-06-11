# Procesamiento documental → JSON validado

Demo que convierte un documento de texto sin estructura (un email, una factura, una nota) en datos limpios y predecibles en formato JSON, con validaciones automáticas. Hecho con IA.

**Demo en vivo:** https://morenoxabi.github.io/demo-documento-json

---

## El problema real

Una empresa recibe cientos de documentos escritos de cualquier manera: pedidos por email, facturas, notas de clientes. Meter esos datos a mano en un sistema es lento y se cuela algún error. El reto no es que la IA "entienda" el texto, es conseguir que devuelva **siempre la misma estructura fiable**, lista para una base de datos. Una cosa es usar la IA y otra es dominarla.

## Qué hace

1. Lees un documento desordenado de entrada.
2. Un modelo de IA extrae los datos siguiendo un esquema fijo.
3. La salida es un JSON limpio (número de pedido, cliente, líneas, totales).
4. Se ejecutan validaciones automáticas para garantizar que el resultado es correcto.

## La clave: el esquema y las reglas

El valor no está en el modelo, está en cómo se le instruye. El demo le pasa al modelo un esquema exacto y un conjunto de reglas, por ejemplo:

- Normalizar la fecha a formato ISO (`YYYY-MM-DD`).
- Usar punto decimal, nunca coma.
- `subtotal = cantidad × precio_unitario`.
- `total = suma de subtotales + envío`.
- Si un dato no aparece, devolver `null`. Nunca inventar valores.

## Validaciones automáticas

Tras la extracción, el código comprueba que el resultado cumple las reglas:

- Campos obligatorios presentes.
- Fecha en formato ISO válido.
- Email del cliente con formato correcto.
- Cada línea: `subtotal` coincide con `cantidad × precio`.
- `total` coincide con la suma de subtotales más el envío.

Si algo no cuadra, se marca en rojo. Salida fiable o no hay salida.

## Tecnología

- HTML, CSS y JavaScript, sin dependencias.
- Funciona como demo estática (con un ejemplo incluido) en GitHub Pages.
- Modo en vivo opcional: conexión a la API de Anthropic (Claude) usando tu propia clave, que se queda solo en el navegador.

## Cómo usarlo

- **Modo demo:** abre la página y pulsa "Extraer a JSON". Funciona con el ejemplo incluido, sin configurar nada.
- **Modo en vivo:** despliega "Modo en vivo", pega tu clave de Anthropic y procesa cualquier texto libre.

## Próximos pasos

- Ampliar el esquema a otros tipos de documento (contratos, albaranes).
- Conectar la salida a una hoja de cálculo o base de datos vía Make o n8n.

---

Hecho por **Xabi Moreno** · IA aplicada, automatización y procesamiento de datos.
[Portfolio](https://morenoxabi.github.io/PORTFOLIO) · [LinkedIn](https://linkedin.com/in/xabi-moreno)
