# Reglas para la Visualización del Flujo de Energía en el Diagrama Sankey

Estas son las convenciones que gobernarán el comportamiento del diagrama de flujo dinámico.

## Regla 1: Estructura de Nodos

*   **Jerarquía:** El diagrama se compone de Nodos Padres (columnas verticales) que representan etapas del proceso (ej. "Producción", "Importación", "Transformación").
*   **Contenido:** Cada Nodo Padre contiene Nodos Hijos, que son los energéticos individuales (ej. "Petróleo crudo", "Gasolinas y naftas").
*   **Orden y Color:** Cada energético (Nodo Hijo) tiene un color y un orden de aparición fijos en toda la simulación, definidos por la lista maestra, para mantener la consistencia visual.

## Regla 2: Dirección y Grosor del Flujo

La visualización de cada flujo de energía se basa en el valor numérico del energético en un nodo.

*   **Flujo de Salida (Positivo > 0):**
    *   Si un energético en un nodo tiene un valor positivo, representa una salida.
    *   El flujo nacerá en este nodo y viajará hacia el siguiente nodo en la cadena.

*   **Flujo de Entrada (Negativo < 0):**
    *   Si un energético tiene un valor negativo, representa una entrada.
    *   El flujo nacerá en el nodo anterior y viajará hacia este nodo.

*   **Grosor del Flujo:**
    *   El grosor de cada línea de flujo será directamente proporcional al valor absoluto del energético (|valor|). Un valor más alto resultará en un flujo más grueso.

## Regla 3: Lógica de Conexión (Inteligente)

Las conexiones entre nodos se adaptan según el estado de expansión de los Nodos Padres.

*   **Padre a Padre (Colapsados):**
    *   Si tanto el nodo de origen como el de destino están colapsados, se muestra un único flujo agregado. El valor de este flujo es la suma de todos los valores de salida del nodo origen.

*   **Hijos a Padre (Origen expandido, Destino colapsado):**
    *   Los flujos nacen de cada Nodo Hijo visible en el origen y todos convergen en el único Nodo Padre del destino.

*   **Hijo a Hijo (Ambos expandidos):**
    *   Es el modo más detallado. El sistema intentará conectar Nodos Hijos con el mismo nombre entre el origen y el destino. Por ejemplo, el flujo de "Producción -> Petróleo crudo" conectará directamente con "Energéticos Primarios -> Petróleo crudo".

## Regla 4: Visualización y Ocultamiento

*   **Valores Cero:** Un Nodo Hijo cuyo valor para el año seleccionado sea 0 no se mostrará en la lista de su Nodo Padre.
*   **Flujos Cero:** Consecuentemente, no se dibujará ningún flujo de energía para los energéticos con valor cero.

## Regla 5: Interactividad

*   **Selector de Año:** Es el control principal. Al cambiar el año, todos los valores se actualizan y el diagrama se redibuja completamente siguiendo estas reglas.

*   **Expansión (+/-):** Al hacer clic en el botón + de un Nodo Padre o Hijo, se muestran u ocultan sus acciones o sub-nodos, y la lógica de conexión (Regla 3) se actualiza para reflejar este nuevo nivel de detalle.

*   **Foco y Flujo Dirigido:** Al hacer clic en un nodo (padre o hijo), este se convierte en el único origen del flujo de energía. El flujo global se detiene y solo se visualizará el camino de la energía hacia adelante desde el nodo seleccionado.

*   **Reinicio del Flujo Global:** Al hacer clic en cualquier área fuera de los nodos, la simulación se restablece a su estado inicial. El foco se elimina y todos los flujos de energía vuelven a mostrarse simultáneamente para el año seleccionado.