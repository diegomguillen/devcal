# DEVCALC Calculadora para desarrolladores de Software

## Introducción

**DEVCALC** es una aplicación web de tipo serverless diseñada específicamente para ingenieros de software embebido y validadores de hardware. La herramienta permite la manipulación de datos a nivel de bit, la evaluación de expresiones complejas con sintaxis compatible con el estándar C y la visualización didáctica de operaciones aritmético-lógicas en arquitecturas de ancho de palabra fijo.

La interfaz está optimizada para su ejecución tanto en entornos de escritorio como en dispositivos móviles (Android), proporcionando un control granular sobre registros de 8, 16 y 32 bits.

Funcionalidades Principales

**1. Sistema de Entrada Multiformato**

El analizador léxico identifica automáticamente la base numérica mediante los siguientes prefijos:

Hexadecimal: 0x o h (ej. 0xFF, hA5).

Binario: 0b o b (ej. 0b1010, b1100).

Octal: o (ej. o755).

Decimal: Entrada directa o prefijo d (ej. 1024, d255).

**2. Motor de Evaluación Basado en Precedencia C**

La calculadora utiliza un analizador sintáctico (Recursive Descent Parser) que respeta la jerarquía de operadores del lenguaje C, de menor a mayor prioridad:
|| → && → | → ^ → & → <</>> → ~

**3. Visualización Didáctica Multilínea**

A diferencia de las calculadoras convencionales, el Bitboard genera dinámicamente filas independientes para:

* Operandos: Desglose visual de los componentes de la operación.

* Resultado: Fila interactiva final donde se pueden conmutar bits manualmente para observar cambios en tiempo real.

## Fundamentos Matemáticos y Lógicos

### Truncamiento y Enmascaramiento

Cada operación es sometida a un proceso de truncamiento basado en el ancho de palabra seleccionado ($W$), asegurando que el sistema se comporte como un registro físico de hardware. La máscara de bits ($M$) se define mediante:

$$M = 2^{W} - 1$$


El resultado final ($R$) tras la evaluación de la expresión ($V$) se calcula como:

$$R = V \land M$$


### Modos de Signo

UNSIGNED: El valor se interpreta como un entero positivo puro.

SIGNED: Se utiliza la representación de complemento a dos. Si el bit más significativo (MSB) es igual a 1, el valor decimal se calcula como:

$$V_{signed} = V - 2^{W}$$


## Atajos de Teclado y Control de Desplazamiento

La aplicación integra funciones de desplazamiento rápido (Shift) mapeadas para una operación ágil:

Tecla

Acción

Etiqueta Visual

AvPág (PageDown)

Desplazamiento a la izquierda (LSH)

<< LSH(AvPag)

RePág (PageUp)

Desplazamiento a la derecha (RSH)

RSH(RePag) >>

El Operando ans

El sistema reserva el token ans (insensible a mayúsculas) para almacenar el último resultado validado. Esto permite encadenar operaciones complejas, tales como:
(ans << 2) | 0x0F

Instalación y Despliegue

Al ser una aplicación serverless autocontenida en un único archivo HTML, el despliegue no requiere de dependencias externas ni servidores de backend:

Clonar el repositorio.

Abrir index.html en cualquier navegador web moderno.

Descargo de Responsabilidad (Disclaimer)

El software se proporciona "tal cual", sin garantía de ningún tipo, expresa o implícita. Dado que esta herramienta puede ser utilizada en la validación de hardware y desarrollo de firmware:

El autor no se hace responsable de errores de cálculo derivados de la implementación del motor de lógica o de interpretaciones erróneas de la sintaxis.

No se recomienda su uso como única fuente de validación en sistemas críticos de seguridad (safety-critical systems) donde fallos en el cálculo puedan derivar en daños materiales o personales.
