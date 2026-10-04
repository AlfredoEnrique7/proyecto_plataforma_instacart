# Proyecto plataforma Instacart


## Descripcción
**Instacart** es una plataforma de entregas de comestibles donde la clientela puede registrar un pedido y hacer que se lo entreguen, similar a Uber Eats y Door Dash.

El conjunto de datos proporcionado para analizar en este caso tiene modificaciones con respecto al original. Se redujo el tamaño del conjunto para que los cálculos se hicieran más rápido y se introdujeron valores ausentes y duplicados. Se tuvo cuidado de conservar las distribuciones de los datos originales cuando se hicieron los cambios.

El objetivo de la fase inicial es realizar una auditoría técnica y diagnóstica sobre el estado de los cinco conjuntos de datos proporcionados. Se busca comprender la estructura de las tablas, corregir los formatos de almacenamiento y verificar la coherencia lógica de las variables antes de aplicar cualquier alteración o limpieza definitiva. Estas acciones están dirigidas a elaborar un informe que aporte valor y claridad sobre los patrones de consumo de comestibles de los usuarios de **Instacart**.

## Conclusiones
### Conclusiones sobre la calidad y el preprocesamiento de los Datos
* **Integridad estructural alcanzada:** La base de datos original presentaba serios desafíos de calidad, incluyendo delimitadores no estándar (`;`) y la presencia de registros duplicados idénticos en la tabla `df_orders`. Mediante técnicas avanzadas de filtrado y el uso de `.drop_duplicates()`, se eliminaron de forma definitiva las redundancias, garantizando la integridad referencial y un contador de `0` duplicados restantes en las claves primarias de todo el ecosistema.
* **Descubrimiento de patrones en valores ausentes:** Se demostró que la ausencia de información en este dataset no obedeció a pérdidas aleatorias, sino a eventos lógicos del negocio y limitaciones de software:
  * En `df_orders`, el 100% de los nulos en los días transcurridos corresponden de forma natural al primer pedido de clientes nuevos (`order_number == 1`), por lo que se mantuvieron intactos.
  * En `df_products`, los nombres vacíos estaban aislados al 100% en el pasillo 100 y departamento 21 (ambos llamados oficialmente *'missing'*), fungiendo como categorías "comodín" del sistema, los cuales se estandarizaron de manera segura bajo la etiqueta `'Unknown'`.
  * En `df_order_products`, las celdas vacías en la secuencia del carrito correspondieron a una limitación técnica (efecto desbordamiento) del software de origen al superar los 64 artículos por orden. Se neutralizó la anomalía usando el valor bandera `999`.
* **Optimización técnica del entorno:** La conversión masiva de identificadores (IDs) y contadores al tipo entero nativo (`int64` / `Int64`) bajo las directrices modernas de Pandas, eliminó eficientemente las advertencias de asignación encadenada, redujo drásticamente el uso de memoria RAM en el servidor y maximizó la velocidad de los cruces relacionales (`merge`).

---

### Conclusiones sobre el comportamiento del consumidor
* **Validación de sensibilidad comercial:** Las estampas de tiempo demostraron un comportamiento comercial puramente orgánico y humano. Los pedidos y la afluencia de personas únicas se concentran con fuerza en horarios puramente diurnos y vespertinos (**entre las 10:00 a.m. y las 4:00 p.m.**), mientras que la madrugada actúa como una zona de inactividad natural, lo que valida la autenticidad de la información recolectada.
* **Dinámica semanal y rutinas de abastecimiento:** Los usuarios prefieren realizar el abastecimiento mayor de la despensa familiar los días **domingos y lunes** (días 0 y 1), experimentando una desaceleración a mitad de semana. La comparación horaria demostró que el miércoles las compras inician más temprano debido a la prisa de la jornada laboral, mientras que los sábados la demanda se toma con más calma, distribuyéndose en forma de meseta hacia el mediodía y la tarde.
* **Ciclos de retención y fidelidad:** El análisis de tiempo de espera evidenció picos de frecuencia exactos en los **días 7, 14, 21 y 28**, confirmando que los hábitos de consumo están firmemente sincronizados con el calendario de la semana y la quincena. Asimismo, la distribución de pedidos por cliente posee un sesgo a la derecha, indicando que el grueso del negocio se sostiene gracias a un núcleo leal de súper usuarios recurrentes, a pesar del truncamiento informático detectado en el tope de la orden 100.

---

### Conclusiones sobre las preferencias del catálogo y recomendaciones de negocio
* **Dominio de productos perecederos y orgánicos:** El ranking de ventas está liderado de forma absoluta por las **bananas (plátanos)** y una abrumadora mayoría de frutas y verduras frescas de vida útil corta que requieren reposición constante. Además, la alta presencia de la etiqueta *"Organic"* define un perfil de consumidor digital de nivel socioeconómico medio-alto, con una marcada preferencia por la alimentación saludable y el bienestar.
* **El impulso de la necesidad primaria (Posición #1):** El primer artículo que entra al carrito de compras actúa como el detonador u objetivo principal que hizo al cliente abrir la aplicación (comúnmente plátanos o lácteos indispensables). Las personas inician su sesión con un enfoque funcional enfocado en la necesidad y postergan los "antojos" o bienes secundarios para las etapas intermedias de navegación.
* **Estrategia de retención individualizada:** Se descubrió que la mitad de los compradores recurrentes vuelven a clonar entre el **30% y el 40%** de su lista de supermercado anterior. Para maximizar los ingresos, se recomienda a los equipos de desarrollo e interfaz (UX) colocar un botón de acceso directo como *"Comprar mi mercado de siempre"* o *"Clonar última orden"* para el segmento maduro, reduciendo la fricción en el embudo de conversión.
* **Protección de stock crítico:** Identificar que los productos básicos diarios poseen tasas de recompra superiores al 70% u 80% convierte a estas categorías en el inventario más crítico de la compañía. Se concluye que asegurar el abastecimiento de estos artículos "ancla" en los almacenes es vital, ya que su desabasto provocaría de forma inmediata la cancelación de carritos completos y la fuga de clientes hacia la competencia.

## Tecnologías utilizadas
* Python (Pandas, Matplotlib, NumPy)
* Jupyter Notebook

## Ver el análisis completo
👉 [Haz clic aquí para ver el código y los gráficos interactivos](proyecto_plataforma_instacart.ipynb)

