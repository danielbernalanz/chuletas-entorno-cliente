# Chuleta examen — Entorno Cliente (RA1, RA2, RA3)

> Basada en las UD 1–4 del curso y en el cuestionario
> "Examen Teórico-Práctico 1ª Evaluación RA 3 SIMULACIÓN CLASE" (6 preguntas).

---

## RA1 — Arquitecturas y herramientas de programación en cliente

### Modelo cliente-servidor
Tres elementos:

- **Servidor**: hardware/software y tecnologías: CGI, APIs, PHP/ASP, servlets Java,
  módulos Apache (`mod_access` control de acceso, `mod_actions` ejecuta CGI/HTTP,
  `mod_auth` autenticación).
- **Cliente**: navegador + HTML, CSS, JavaScript, ActiveX.
- **Red**: protocolos y conectividad.

### Características de JavaScript
- Lenguaje de **script interpretado** (se ejecuta sentencia a sentencia, sin compilar).
- **Débilmente tipado y dinámico**: no se declara el tipo y puede cambiar en ejecución.
- **Orientado a objetos** y **orientado a prototipos**.
- **Imperativo y estructurado** (secuencia, selección, iteración).
- **No sustituye al servidor**: no puede escribir ficheros en el servidor; sí puede
  solicitar ficheros. La web debe funcionar aunque JS esté desactivado.
- El código es **visible**; la ofuscación (`javascriptobfuscator.com`) es reversible.

### Las 4 capas del desarrollo web cliente
1. Comportamiento → JavaScript
2. Presentación → CSS
3. Estructura → DOM / HTML
4. Contenido → texto, imágenes, vídeo

### Las 4 tecnologías base
HTML (estructura), CSS (presentación), JavaScript (comportamiento),
AJAX (integración asíncrona cliente-servidor).

### Arquitectura de un navegador
- Subsistema de **interfaz de usuario**.
- **Motor de navegación** (interfaz de alto nivel).
- **Motor de renderizado** (representación visual del recurso).
- **Subsistema de comunicaciones** (HTTP, FTP, HTTPS...).
- **Intérprete de JavaScript**.
- **Parser XML** (árbol en memoria de la página).
- **Componente de visualización**.
- **Subsistema de persistencia de datos**.

### Criterios de clasificación de navegadores
Plataforma/SO, características, personalización/accesibilidad, soporte de estándares,
licencia (software libre o propietario).

### Navegadores
- **Firefox**: código abierto, multiplataforma.
- **Chrome**: compilado a partir de componentes de código abierto.
- **Safari**: navegador por defecto de Apple.
- **Opera**: propietario con componentes abiertos; escritorio Windows/Mac/Linux,
  móvil iOS/Android.

### Lenguajes y tecnologías
- **HTML**: lenguaje de marcas, interpretado, hipervínculos.
- **XML**: describe y transfiere datos; no los muestra.
- **XHTML**: adaptación de HTML a XML.
- **DHTML**: HTML + JavaScript + CSS + DOM.
- **CSS**: separa el formato de la estructura.
- **AJAX**: técnicas asíncronas; hoy se usa JSON más que XML.
- **Flash/ActionScript** y **applets Java** (Chrome y Edge ya no los soportan).

### Consola y entorno
- Chrome: `Ctrl+Shift+I`.
- Firefox: `Ctrl+Shift+K`.
- VS Code + extensión JavaScript + Prettier.

### Vocabulario
- **Lenguaje**: forma de escribir el programa (Angular → TypeScript;
  Symfony/Laravel → PHP; Spring → Java).
- **Librería**: dependencia para una funcionalidad (jQuery).
- **Framework**: caja de herramientas para montar el proyecto.
- **VanillaJS**: JavaScript puro.
- **Frontend** = cliente; **Backend** = servidor.

### Integrar JavaScript en HTML (3 formas)
1. `<script>...</script>` en el propio documento.
2. Fichero externo `.js` con `<script src="...">` (sin límite de ficheros).
3. En atributos HTML (`onclick="..."`); peor mantenimiento.

**Ventajas del fichero externo**: carga más rápida (caché), separación
estructura/comportamiento, depuración y mantenimiento, modularidad, seguridad.

---

## RA2 — Introducción a JavaScript

### Identificadores
- Solo letras, números, `$` y `_`.
- El primer carácter **no** puede ser número ni `@`.
- `@` no está permitido en **ninguna** posición.
- `let 10_nombre` y `let mi@nombre` son incorrectos.

### var / let / const
| | Ámbito | Reasignable | Hoisting |
|---|---|---|---|
| `var` | global/función (no bloque) | sí | sí |
| `let` | global/función/bloque | sí | no (TDZ) |
| `const` | global/función/bloque | no | no |

- `const` no se reasigna, pero el contenido de objetos/arrays es **mutable**.
- `var` en bucles anidados comparte la misma variable y se pisa.
- `let` crea una variable nueva por bloque.

### Hoisting
```js
console.log(x); // undefined (var declarada, sin inicializar)
var x = 1;
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 1;
```

### typeof
```js
typeof undefined // "undefined"
typeof null      // "object"   ← trampa
typeof "cadena"  // "string"
typeof 15        // "number"
typeof true      // "boolean"
```

### undefined vs null
- `undefined`: no existe / nunca se asignó valor.
- `null`: existe y se asignó explícitamente sin valor.
- `undefined == null` → `true` (coerción).
- `undefined === null` → `false`.

### NaN
- `NaN === NaN` → `false`; `NaN == NaN` → `false`.
- Comprobar con `isNaN()` o `Number.isNaN()`.

### == vs ===
- Usa siempre `===`.
- Con `==`: mismo tipo → igual que `===`; string vs número → convierte el string;
  booleano vs otro → convierte a número.
- `'' == 0` → true; `'5' == 5` → true; `false == 0` → true.

### Strings
- Comillas simples, dobles o backticks.
- `length` cuenta caracteres: `"Mi\n".length` → **3**.
- **Inmutables**: no se cambia un carácter; se reasigna la variable.
- `s[-1]` → `undefined`; `s.at(-1)` → último carácter.
- Escapes: `\n`, `\r`, `\t`, `\v`, `\'`, `\"`, `\\`, `\xdd`, `\u0008`.
- Template literals: `` `1 + 2 = ${1 + 2}.` `` → evalúa la expresión.

### Números
- Conversión global: `Number()`, `parseInt()`, `parseFloat()`.
- `parseInt(str, base)`: base 2–36; admite prefijo `0x` en base 16.
- `parseInt('2n9c', 36)` → `123456`; `parseInt('0xff', 16)` → `255`.

### Entrada/salida
- `alert()`, `confirm()` (true/false), `prompt()` (string o null).
- Comentarios: `//` y `/* */`.

---

## RA3 — Objetos predefinidos, funciones, arrays y objetos

### Date
- `getDate()` 1–31; `getMonth()` **0–11** (+1); `getFullYear()`; `getDay()` 0=domingo.
- `toLocaleTimeString()`, `toLocaleDateString()`.
- Reloj: `setInterval(fn, 1000)` / `clearInterval(id)`.

### Math
- `Math.PI`, `Math.E`, `Math.exp(x)`, `Math.pow(base, exp)`, `Math.sqrt(x)`, `Math.abs(x)`.
- `Math.random()` → `[0, 1)`.
- `Math.max(...arr)` / `Math.min(...arr)`.
- Redondeos con negativos:
```js
Math.floor(-1.6) // -2  (abajo)
Math.ceil(-1.6)  // -1  (arriba)
Math.round(-1.6) // -2  (más cercano)
Math.trunc(-1.6) // -1  (quita decimales)
```

### Number
- `MAX_VALUE`, `MIN_VALUE`, `MAX_SAFE_INTEGER` = `9007199254740991`.
- `NaN`, `POSITIVE_INFINITY`, `NEGATIVE_INFINITY`.
- `toFixed(n)` → **string** con n decimales (rellena con ceros); `+` unario lo hace number.
- `toPrecision(n)` → string con n cifras significativas.
- `BigInt`: `10n` o `BigInt()`; no mezclar con Number ni con Math; usar `**`.

### String — métodos
- `length`, `toString()`, `concat()`.
- `toUpperCase()`, `toLowerCase()`.
- `indexOf()` → posición o **-1**; `lastIndexOf()`.
- `substring(inicio, fin)` → fin **excluido**; negativos → 0; intercambia si inicio > fin.
- `slice(inicio, fin)` → acepta negativos (desde el final).
- `split(sep)` → array; sin argumento separa por coma; `split("")` → letras.
- `replace()` → solo la primera coincidencia; `replaceAll()`.
- `charAt(i)`, `charCodeAt(i)`.
- `includes()`, `startsWith()`, `endsWith()`, `trim()`, `repeat()`, `padStart()`, `padEnd()`.

### Array
- `length` modificable: `arr.length = 0` **vacía**; subirla después **no recupera** valores.
- `push()`/`pop()` final; `unshift()`/`shift()` inicio.
- `indexOf()`, `includes()`, `join(sep)`.
- `slice()` → copia sin mutar; `splice()` → muta (borra/inserta).
- `sort()` → **muta** y ordena como **strings** por defecto; numérico: `(a, b) => a - b`.
- `reverse()` → muta.
- `at(-1)` → último; `arr[-1]` → `undefined`.
- **Referencia**: `let cart = fruits` copia la referencia. Copiar: `[...arr]`,
  `structuredClone()`.

### Objetos nativos
- **Boolean**: `new Boolean(false)` es un objeto **truthy**.
- **Object**: `keys()`, `values()`, `entries()`, `assign(destino, fuente)`, `freeze()`.
- **JSON**: `JSON.stringify(obj)` ↔ `JSON.parse(texto)`.
- **Promise**: `then()`, `catch()`, `finally()`, `Promise.all()`, `Promise.race()`.

### Map y Set
```js
const mapa = new Map();
mapa.set("nombre", "Ana");
mapa.set("edad", 25);
mapa.set("nombre", "Luis"); // sobrescribe la clave
mapa.size;                  // 2
mapa.get("nombre");         // "Luis"
mapa.get("pais");           // undefined (no null, no error)
mapa.has("edad");           // true
mapa.delete("edad");
mapa.clear();
```
- `Map`: claves únicas y de cualquier tipo.
- `Set`: valores únicos; `add`, `delete` (true/false), `has`, `size`, `clear`.
- Deduplicar: `[...new Set(array)]`.

### Estructuras de control
- `if / else if / else`, `switch` con `break` y `default`.
- `for`, `while`, `do-while`.
- `for-in` → **índices/claves**; `for-of` → **valores** (no objetos literales).
- `break`, `continue`, `return`.

### Objetos de alto nivel (BOM)
Jerarquía: `window` → `document`, `navigator`, `screen`, `history`, `location`.

- **window**: `innerWidth/innerHeight`, `alert/confirm/prompt`, `open/close`,
  `setTimeout/clearTimeout`, `setInterval/clearInterval`, `scrollTo`,
  `localStorage/sessionStorage`.
- **navigator**: `appCodeName`, `appName`, `appVersion`, `cookieEnabled`, `platform`,
  `userAgent`, `plugins`.
- **screen**: `height`, `width`, `availHeight`, `availWidth`, `colorDepth`, `pixelDepth`.
- **history**: `length`, `back()`, `forward()`, `go(n)`.
- **location**: `href`, `protocol`, `host`, `hostname`, `port`, `pathname`, `search`,
  `hash`; `reload()`, `replace()`, `assign()`.
- **document**: `getElementById()`, `getElementsByName()`, `getElementsByTagName()`,
  `write()`, `writeln()`, `cookie`, `title`, `URL`, `referrer`;
  colecciones `forms[]`, `images[]`, `links[]`, `anchors[]`.

### Almacenamiento web
- `localStorage` → **no expira**.
- `sessionStorage` → se borra al cerrar sesión/navegador.
- ≥ **5 MB**; nunca se envía al servidor; más seguro que las cookies.
- `setItem`, `getItem`, `removeItem`, `clear`.
- Comprobar soporte: `typeof(Storage) !== "undefined"`.

### Funciones
- `function nombre(params) { return ... }`; `return` corta la ejecución.
- Nº de argumentos puede diferir del declarado; `arguments` (no existe en arrow).
- Valores por defecto: solo si falta o es `undefined`.
- Parámetro requerido: valor por defecto que lanza `throw new Error(...)`.
- **Arrow**: `(a, b) => a + b`; anónimas; sin `arguments`; `this` léxico.
- **Spread `...`**: concatenar/copiar arrays, string → array, fusionar objetos
  (gana el último), pasar argumentos.

### Objetos propios
1. **Literal**: `{ marca: "LG", peso: 5 }`.
2. **new Object()**.
3. **Función constructora** + `new`.
- `this` es **dinámico**: depende de cómo se llama la función.
- JavaScript usa **prototipos**, no clases reales.

### Programación funcional
```js
reservas.every(r => r.pagada);           // true si TODOS cumplen
reservas.some(r => r.pagada);            // true si AL MENOS UNO cumple
reservas.filter(r => !r.pagada);         // array con los que cumplen
reservas.find(r => r.id === 10002);      // primer elemento o undefined
reservas.findIndex(r => r.id === 10002); // índice o -1
reservas.map(r => r.precio * 0.9);       // nuevo array transformado
reservas.reduce((total, r) => total + r.precio, 0); // acumula
```
- `every/filter/find/findIndex/map/reduce/some` **no mutan**.
- Módulos: `export` / `import`; en HTML `<script type="module">`.

---

## Cuestionario RA3 — preguntas y respuestas

### Pregunta 1 — Strings inmutables y template literals
```js
let str = `Mi\n`;
console.log(str.length);        // 3
let s = 'Hola';
s = 'h' + s[1] + s[2] + s[3];
console.log(s, s[-1]);          // hola undefined
console.log(`1 + 2 = ${1 + 2}.`); // 1 + 2 = 3.
```
**Correcta: f** (`3` / `hola undefined` / `1 + 2 = 3.`).
- `\n` es un solo carácter.
- El `.` final es texto literal, no operador.
- `s[-1]` no da el último carácter; para eso `at(-1)`.

### Pregunta 2 — sort y map
```js
let a = [1, 2, 15];
a.sort();                 // [1, 15, 2]
a.sort((x, y) => y - x);  // [15, 2, 1]
["Bilbo","Gandalf","Nazgul"].map(i => i.length); // [5, 7, 6]
```
**Correcta: e** (`1,15,2` / `15,2,1` / `5,7,6`).
- `sort()` sin comparador ordena como texto (`"15" < "2"`).
- `sort()` muta el array.
- `map` devuelve un array nuevo con las longitudes.

### Pregunta 3 — Math y toFixed
```js
Math.floor(-1.6) // -2
Math.ceil(-1.6)  // -1
Math.round(-1.6) // -2
Math.trunc(-1.6) // -1
price.toFixed(5)          // "12.34000" (string)
typeof price.toFixed(5)   // "string"
typeof +price.toFixed(5)  // "number"
```
**Correcta: a** (`-2 -1 -2 -1` / `12.34000 string number`).

### Pregunta 4 — Referencia de arrays y length
```js
let fruits = ["Apples", "Pear", "Orange"];
let cart = fruits;
cart.push("Banana");
fruits.length;      // 4
fruits.length = 0;  // vacía el array
cart.length;        // 0
cart.at(-1);        // undefined
cart[-1];           // undefined
fruits.length = 5;
fruits[3];          // undefined
fruits.length;      // 5
```
**Correcta: f** (`4` / `0 undefined undefined` / `undefined 5`).
- `cart` y `fruits` apuntan al mismo array.
- Truncar es irreversible: los valores no vuelven.

### Pregunta 5 — Map
```js
mapa.set("nombre", "Ana");
mapa.set("edad", 25);
mapa.set("nombre", "Luis");
mapa.size;          // 2
mapa.get("nombre"); // "Luis"
mapa.get("pais");   // undefined
```
**Correcta: d** (`2` / `Luis` / `undefined`).
- Claves únicas: `set` sobrescribe.
- Clave inexistente → `undefined`, no `null` ni error.

### Pregunta 6 — Literales numéricos y parseInt
```js
0b101                  // 5
1_000                  // 1000
(255).toString(16)     // "ff"
parseInt('2n9c', 36)   // 123456
parseInt('0xff', 16)   // 255
```
**Correcta: b** (`5 1000` / `ff` / `123456 255`).

---

## Trampas típicas

1. `typeof null` → `"object"`.
2. `NaN !== NaN`; usar `isNaN`.
3. `sort()` sin comparador ordena como texto.
4. `Math.round(-1.6)` → `-2`; `Math.trunc(-1.6)` → `-1`.
5. `toFixed()` devuelve **string**.
6. `arr.length = 0` vacía y no se recupera.
7. `let b = a` en arrays/objetos copia la **referencia**.
8. `Map.get` inexistente → `undefined`; `set` repetido sobrescribe.
9. `s[-1]` → `undefined`; usar `at(-1)`.
10. `substring` no acepta negativos; `slice` sí.
11. `for-of` no recorre objetos literales; `for-in` da claves.
12. `new Boolean(false)` es truthy.
13. `const` impide reasignar, no mutar.
14. `var` no respeta ámbito de bloque; `let` sí.
15. `localStorage` no expira; `sessionStorage` sí.

---

## Ejercicio tipo examen: registro + tabla + localStorage

Archivo de referencia: `Descargas/posible examen js.html`.

### Estructura
- Formulario con inputs `nombre`, `fechaNac` (`type="date"`), `nota` (`type="number" step="0.1"`).
- Botones `type="button"` con `onclick`: no envían el formulario, no hace falta `preventDefault()`.
- Tabla con `<tbody id="cuerpoTabla">` vacío; filas por `insertRow()`.
- Párrafos `#mensajeError` y `#infoEstadisticas`.

### Validación
- Salir pronto: `if (cond) { msg.innerHTML = "..."; return; }`.
- Nombre: `campoNombre.length < 3`.
- Obligatorios: `campoFecha === "" || campoNota === ""`.

### Cálculo de edad con Date
```js
let nac = new Date(campoFecha);
let hoy = new Date();
let edad = hoy.getFullYear() - nac.getFullYear();
let mes = hoy.getMonth() - nac.getMonth();
if (mes < 0 || (mes === 0 && hoy.getDate() < nac.getDate())) edad--;
if (edad < 0) { /* fecha futura */ }
```

### Number y Math
```js
let numNota = parseFloat(campoNota);
let notaFormateada = numNota.toFixed(2); // string
let id = Math.floor(Math.random() * 9000) + 1000; // 1000–9999
```

### Insertar fila (DOM clásico)
```js
let tbody = document.getElementById("cuerpoTabla");
let fila = tbody.insertRow(-1);        // -1 = al final
fila.insertCell(0).innerHTML = id;
fila.insertCell(1).innerHTML = nombre.toUpperCase();
fila.insertCell(2).innerHTML = edad;
fila.insertCell(3).innerHTML = notaFormateada;
```

### localStorage
```js
localStorage.setItem("total_alumnos", totalRegistros);
let total = Number(localStorage.getItem("total_alumnos")); // al cargar
localStorage.removeItem("total_alumnos");                  // vaciar
```
- Recuperar en `window.onload`.
- Tras insertar: `document.getElementById("miFormulario").reset()`.
- Vaciar todo: `tbody.innerHTML = ""`, contadores a 0 y `removeItem`.
