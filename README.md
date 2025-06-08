# Happy Path
Apertura de la ventana del chatbot

Precondición: El usuario está en la LandingPage y el icono flotante del chatbot (burbuja) es visible en la esquina inferior.

Acción: El usuario hace clic en la burbuja del chatbot.

Resultado esperado: La ventana del chat aparece con una animación suave, mostrando un mensaje de bienvenida del bot. El icono de la burbuja cambia a una "X" para indicar la opción de cierre.

El usuario puede escribir una consulta

Precondición: La ventana del chat está abierta.

Acción: El usuario escribe una pregunta en el campo de texto, por ejemplo: "¿Cómo me registro como freelancer?".

Resultado esperado: El texto ingresado por el usuario es visible y se actualiza correctamente en el campo de texto.

El usuario envía la consulta y recibe una respuesta

Precondición: El usuario ha escrito una pregunta válida en el campo de texto.

Acción: El usuario hace clic en el botón "Enviar" (o presiona Enter).

Resultado esperado:

El mensaje del usuario aparece inmediatamente en la ventana de chat, alineado a un lado (ej. derecha).

El campo de texto se vacía, quedando listo para una nueva consulta.

Aparece un indicador de que el bot está "pensando" o procesando.

En pocos segundos, se realiza una llamada a la API de OpenAI y la respuesta generada por la IA se muestra en la ventana de chat como un nuevo mensaje del bot, alineado al lado opuesto (ej. izquierda).

La conversación puede continuar

Precondición: El bot ha dado una respuesta.

Acción: El usuario escribe y envía una segunda pregunta de seguimiento.

Resultado esperado: El nuevo mensaje del usuario se añade al final de la conversación, y el bot genera y muestra una nueva respuesta, manteniendo el historial de chat visible y con scroll.

Cierre de la ventana del chatbot

Precondición: La ventana del chat está abierta.

Acción: El usuario hace clic en el icono "X" en la cabecera de la ventana del chat, o vuelve a hacer clic en el icono flotante.

Resultado esperado: La ventana del chat se cierra con una animación suave. El icono flotante vuelve a su estado original (ej. icono de burbuja de chat). El historial de la conversación se mantiene en el estado del componente para que, si el usuario vuelve a abrir el chat, pueda continuar donde lo dejó.

# UNHAPPY PATHS
Fallo en la comunicación con la API de OpenAI

Acción: El usuario envía una pregunta, pero la llamada a la API de OpenAI falla (ej. por un problema de red, API key inválida, o sobrecarga del servicio de OpenAI).

Resultado esperado: El mensaje del usuario aparece en la ventana de chat, pero en lugar de una respuesta de la IA, el bot muestra un mensaje de error amigable como: "Lo siento, no pude procesar tu pregunta en este momento. Por favor, intenta de nuevo en unos instantes." La interfaz no se rompe y el usuario puede intentar enviar un mensaje de nuevo.

El usuario intenta enviar un mensaje vacío

Acción: El usuario hace clic en el botón "Enviar" sin haber escrito ningún texto en el campo de entrada.

Resultado esperado: No ocurre nada. La acción de enviar se previene y no se añade ningún mensaje nuevo a la conversación. Opcionalmente, el campo de texto puede mostrar una animación sutil (ej. un temblor) para indicar que se requiere texto.

La respuesta de la IA es muy larga o contiene formato complejo

Acción: La IA devuelve un texto muy extenso o con un formato inesperado (ej. bloques de código, listas muy largas).

Resultado esperado: La burbuja del mensaje del bot se expande verticalmente para contener todo el texto, y la ventana del chat permite hacer scroll correctamente para ver la respuesta completa sin romper el layout de la página. El formato se sanea para evitar problemas de renderizado.

Timeout de la API

Acción: La API de OpenAI tarda demasiado en responder (ej. más de 15 segundos).

Resultado esperado: El frontend cancela la espera y el bot muestra un mensaje indicando el problema, como: "La respuesta está tardando más de lo esperado. ¿Quieres que siga esperando o prefieres intentar con otra pregunta?". Esto evita que el usuario espere indefinidamente.


# Laboratorio 04: Pruebas Unitarias con Jest en React

Este laboratorio tiene como objetivo proporcionar una introducción práctica a las pruebas unitarias en aplicaciones React utilizando Jest y React Testing Library.

## Aplicación Todo List

La aplicación desarrollada es una lista de tareas (Todo List) con las siguientes funcionalidades:

- Añadir nuevas tareas
- Marcar tareas como completadas
- Eliminar tareas
- Filtrar tareas por estado (todas, activas, completadas)
- Ver estadísticas de tareas
- Borrar todas las tareas completadas

## Estructura del Proyecto

```
app/
├── components/
│   ├── Todo.tsx               # Componente principal que integra todos los demás
│   ├── TodoForm.tsx           # Formulario para añadir nuevas tareas
│   ├── TodoItem.tsx           # Componente individual para cada tarea
│   ├── TodoList.tsx           # Lista de tareas
│   ├── TodoFilter.tsx         # Filtros para las tareas
│   ├── TodoStats.tsx          # Estadísticas de tareas
│   └── __tests__/             # Directorio de pruebas
│       ├── TodoItem.test.tsx  # Pruebas para TodoItem
│       ├── TodoForm.test.tsx  # Pruebas para TodoForm
│       └── TodoList.test.tsx  # Pruebas para TodoList
├── page.tsx                   # Página principal
└── layout.tsx                 # Layout de la aplicación
```

## Instrucciones del Laboratorio

En este laboratorio, exploraremos cómo escribir pruebas unitarias efectivas siguiendo el patrón **Prepare, Execute and Validate**:

1. **Prepare**: Configurar el entorno de prueba y los datos necesarios
2. **Execute**: Realizar la acción que queremos probar
3. **Validate**: Verificar que el resultado es el esperado

### Ejercicios

#### Ejercicio 1: Completar prueba de TodoItem

Completa el test para verificar que el componente `TodoItem` muestra correctamente el texto de una tarea con caracteres especiales.

Archivo: `app/components/__tests__/TodoItem.test.tsx`

#### Ejercicio 2: Completar prueba de TodoForm

Completa el test para verificar que el componente `TodoForm` maneja correctamente la entrada de texto con espacios al inicio o final.

Archivo: `app/components/__tests__/TodoForm.test.tsx`

#### Ejercicio 3: Completar prueba de TodoList

Completa el test para verificar que el componente `TodoList` pasa correctamente las funciones onToggle y onDelete a cada TodoItem.

Archivo: `app/components/__tests__/TodoList.test.tsx`

## Casos de Prueba

En las pruebas existentes, podrás encontrar ejemplos de:

- **Happy Path**: Pruebas que verifican el comportamiento correcto cuando todo funciona como se espera
- **Unhappy Path**: Pruebas que verifican el comportamiento cuando hay situaciones inesperadas o errores

## Ejecución de Pruebas

Para ejecutar las pruebas, utiliza el siguiente comando:

```bash
npm test
```

Para ejecutar las pruebas en modo observador (útil durante el desarrollo):

```bash
npm run test:watch
```

## Recursos Adicionales

- [Jest Documentation](https://jestjs.io/docs/getting-started)
- [React Testing Library Documentation](https://testing-library.com/docs/react-testing-library/intro/)
- [Jest DOM Testing Library](https://github.com/testing-library/jest-dom)
