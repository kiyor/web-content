---
id: linear-decay.md
title: Decaimiento linealCompatible with Milvus 2.6.x
summary: >-
  El decaimiento lineal crea un declive en línea recta que termina en un punto
  cero absoluto en los resultados de búsqueda. Al igual que la cuenta atrás de
  un evento próximo, en la que la relevancia se desvanece gradualmente hasta que
  el evento ha pasado, el decaimiento lineal aplica una reducción predecible y
  constante de la relevancia a medida que los elementos se alejan de su punto
  ideal hasta que desaparecen por completo. Este enfoque es ideal cuando se
  desea una tasa de decaimiento consistente con un límite claro, asegurando que
  los elementos más allá de un cierto límite queden completamente excluidos de
  los resultados.
beta: Milvus 2.6.x
---
<h1 id="Linear-Decay" class="common-anchor-header">Decaimiento lineal<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Linear-Decay" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h1><p>El decaimiento lineal crea un declive en línea recta que termina en un punto cero absoluto en los resultados de búsqueda. Al igual que la cuenta atrás de un evento próximo, en la que la relevancia se desvanece gradualmente hasta que el evento ha pasado, el decaimiento lineal aplica una reducción predecible y constante de la relevancia a medida que los elementos se alejan de su punto ideal hasta que desaparecen por completo. Este enfoque es ideal cuando se desea una tasa de decaimiento consistente con un límite claro, asegurando que los elementos más allá de un cierto límite queden completamente excluidos de los resultados.</p>
<p>A diferencia de otras funciones de descomposición:</p>
<ul>
<li><p>La descomposición gaussiana sigue una curva de campana que se aproxima gradualmente pero nunca llega a cero.</p></li>
<li><p>La descomposición exponencial mantiene una larga cola de relevancia mínima que se extiende indefinidamente.</p></li>
</ul>
<p>El decaimiento lineal crea de forma única un punto final definitivo, lo que lo hace especialmente eficaz para aplicaciones con límites naturales o fechas límite.</p>
<h2 id="When-to-use-linear-decay" class="common-anchor-header">Cuándo utilizar el decaimiento lineal<button data-href="#When-to-use-linear-decay" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>El decaimiento lineal es particularmente eficaz para:</p>
<table>
   <tr>
     <th><p>Caso práctico</p></th>
     <th><p>Ejemplo</p></th>
     <th><p>Por qué funciona bien el decaimiento lineal</p></th>
   </tr>
   <tr>
     <td><p>Listados de eventos</p></td>
     <td><p>Plataformas de entradas para conciertos</p></td>
     <td><p>Crea un límite claro para los eventos demasiado lejanos en el tiempo</p></td>
   </tr>
   <tr>
     <td><p>Ofertas por tiempo limitado</p></td>
     <td><p>Ventas flash, promociones</p></td>
     <td><p>Garantiza que no aparezcan ofertas caducadas o a punto de caducar</p></td>
   </tr>
   <tr>
     <td><p>Radio de entrega</p></td>
     <td><p>Entrega de comida, servicios de mensajería</p></td>
     <td><p>Impone límites geográficos estrictos</p></td>
   </tr>
   <tr>
     <td><p>Contenido restringido por edad</p></td>
     <td><p>Plataformas de citas, servicios multimedia</p></td>
     <td><p>Establece umbrales de edad firmes</p></td>
   </tr>
</table>
<p>Elija el decaimiento lineal cuando:</p>
<ul>
<li><p>Tu aplicación tiene un límite natural, una fecha límite o un umbral</p></li>
<li><p>Los elementos que superan un determinado punto deben excluirse completamente de los resultados</p></li>
<li><p>Necesitas una tasa de pérdida de relevancia predecible y constante.</p></li>
<li><p>Los usuarios deben ver una demarcación clara entre los elementos relevantes y los irrelevantes.</p></li>
</ul>
<h2 id="Steady-decline-principle" class="common-anchor-header">Principio de disminución constante<button data-href="#Steady-decline-principle" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>La decadencia lineal crea una caída en línea recta que disminuye a un ritmo constante hasta llegar exactamente a cero. Este patrón aparece en muchos escenarios cotidianos, como los temporizadores de cuenta atrás, el agotamiento del inventario y los plazos en los que la relevancia tiene un claro punto de caducidad.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/linear-decay.png" alt="Linear Decay" class="doc-image" id="linear-decay" />
   </span> <span class="img-wrapper"> <span>Decaimiento lineal</span> </span></p>
<p>El gráfico anterior muestra cómo el decaimiento lineal afectaría a los listados de eventos en una plataforma de venta de entradas:</p>
<ul>
<li><p><code translate="no">origin</code> (fecha actual): El momento actual, donde la relevancia es máxima (1,0).</p></li>
<li><p><code translate="no">offset</code> (1 día): La "ventana de eventos inmediatos": todos los eventos que se celebren en el día siguiente mantienen una puntuación de relevancia completa (1,0), lo que garantiza que los eventos muy inminentes no se vean penalizados por pequeñas diferencias temporales.</p></li>
<li><p><code translate="no">decay</code> (0.5): La puntuación a la distancia de escala: este parámetro controla la tasa de disminución de la relevancia.</p></li>
<li><p><code translate="no">scale</code> (10 días): El periodo de tiempo en el que la relevancia cae hasta el valor de decaimiento-los eventos a 10 días vista tienen sus puntuaciones de relevancia reducidas a la mitad (0,5).</p></li>
</ul>
<p>Como puede ver en la curva rectilínea, los eventos que se produzcan en un plazo superior a 16 días tendrán una relevancia cero y no aparecerán en los resultados de búsqueda. Esto crea un límite claro que garantiza que los usuarios sólo vean los próximos eventos relevantes dentro de una ventana temporal definida.</p>
<p>Este comportamiento refleja cómo funciona normalmente la planificación de eventos: los eventos inminentes son los más relevantes, los eventos de las próximas semanas tienen una importancia decreciente y los eventos demasiado lejanos en el tiempo (o ya pasados) no deberían aparecer en absoluto.</p>
<h2 id="Formula" class="common-anchor-header">Fórmula<button data-href="#Formula" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>La fórmula matemática para calcular la puntuación de la descomposición lineal es</p>
<p>$$ S(doc) = \max\left( \frac{s - \max(0, |fieldvalue_{doc} - origin| - offset)}{s}, 0 \right) $$</p>
<p>Donde:</p>
<p>$$ s = \frac {escala}{(1.0 - decaimiento)} $$</p>
<p>Desglosando esto en lenguaje sencillo:</p>
<ol>
<li><p>Calcular lo lejos que el valor de campo es desde el origen: $|fieldvalue_{doc} - origen|$.</p></li>
<li><p>Restar el desplazamiento (si lo hay), pero nunca por debajo de cero: $\max(0, distancia - desplazamiento)$.</p></li>
<li><p>Determinar el parámetro $s$ a partir de sus valores de escala y decaimiento.</p></li>
<li><p>Restar la distancia ajustada de $s$ y dividir por $s$.</p></li>
<li><p>Asegúrese de que el resultado nunca es inferior a cero: $\max(resultado, 0)$.</p></li>
</ol>
<p>El cálculo de $s$ transforma sus parámetros de escala y decaimiento en el punto en el que la puntuación llega a cero. Por ejemplo, con decaimiento=0,5 y escala=7, la puntuación llegará exactamente a cero en la distancia=14 (dos veces el valor de la escala).</p>
<h2 id="Use-linear-decay" class="common-anchor-header">Utilizar el decaimiento lineal<button data-href="#Use-linear-decay" class="anchor-icon" translate="no">
      <svg translate="no"
        aria-hidden="true"
        focusable="false"
        height="20"
        version="1.1"
        viewBox="0 0 16 16"
        width="16"
      >
        <path
          fill="#0092E4"
          fill-rule="evenodd"
          d="M4 9h1v1H4c-1.5 0-3-1.69-3-3.5S2.55 3 4 3h4c1.45 0 3 1.69 3 3.5 0 1.41-.91 2.72-2 3.25V8.59c.58-.45 1-1.27 1-2.09C10 5.22 8.98 4 8 4H4c-.98 0-2 1.22-2 2.5S3 9 4 9zm9-3h-1v1h1c1 0 2 1.22 2 2.5S13.98 12 13 12H9c-.98 0-2-1.22-2-2.5 0-.83.42-1.64 1-2.09V6.25c-1.09.53-2 1.84-2 3.25C6 11.31 7.55 13 9 13h4c1.45 0 3-1.69 3-3.5S14.5 6 13 6z"
        ></path>
      </svg>
    </button></h2><p>El decaimiento lineal puede aplicarse tanto a la búsqueda vectorial estándar como a las operaciones de búsqueda híbrida en Milvus. A continuación se muestran los fragmentos de código clave para implementar esta función.</p>
<div class="alert note">
<p>Antes de utilizar las funciones de decaimiento, primero debe crear una colección con los campos numéricos apropiados (como marcas de tiempo, distancias, etc.) que se utilizarán para los cálculos de decaimiento. Para ver ejemplos de trabajo completos que incluyan la configuración de la colección, la definición del esquema y la inserción de datos, consulte el <a href="/docs/es/tutorial-implement-a-time-based-ranking-in-milvus.md">Tutorial del Clasificador por Decaimiento</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Crear un clasificador de descomposición</h3><p>Una vez configurada la colección con un campo numérico (en este ejemplo, <code translate="no">event_date</code> como segundos a partir de ahora), cree un clasificador de decaimiento lineal:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Function, FunctionType
<span class="hljs-keyword">import</span> time

<span class="hljs-comment"># Calculate current time</span>
current_time = <span class="hljs-built_in">int</span>(time.time())

<span class="hljs-comment"># Create a linear decay ranker for event listings</span>
ranker = Function(
    name=<span class="hljs-string">&quot;event_relevance&quot;</span>,               <span class="hljs-comment"># Function identifier</span>
    input_field_names=[<span class="hljs-string">&quot;event_date&quot;</span>],     <span class="hljs-comment"># Numeric field to use</span>
    function_type=FunctionType.RERANK,    <span class="hljs-comment"># Function type. Must be RERANK</span>
    params={
        <span class="hljs-string">&quot;reranker&quot;</span>: <span class="hljs-string">&quot;decay&quot;</span>,              <span class="hljs-comment"># Specify decay reranker</span>
        <span class="hljs-string">&quot;function&quot;</span>: <span class="hljs-string">&quot;linear&quot;</span>,             <span class="hljs-comment"># Choose linear decay</span>
        <span class="hljs-string">&quot;origin&quot;</span>: current_time,           <span class="hljs-comment"># Current time</span>
        <span class="hljs-string">&quot;offset&quot;</span>: <span class="hljs-number">12</span> * <span class="hljs-number">60</span> * <span class="hljs-number">60</span>,           <span class="hljs-comment"># 12 hour immediate events window</span>
        <span class="hljs-string">&quot;decay&quot;</span>: <span class="hljs-number">0.5</span>,                     <span class="hljs-comment"># Half score at scale distance</span>
        <span class="hljs-string">&quot;scale&quot;</span>: <span class="hljs-number">7</span> * <span class="hljs-number">24</span> * <span class="hljs-number">60</span> * <span class="hljs-number">60</span>         <span class="hljs-comment"># 7 days (in seconds)</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Aplicar a la búsqueda vectorial estándar</h3><p>Después de definir su decay ranker, puede aplicarlo durante las operaciones de búsqueda pasándolo al parámetro <code translate="no">ranker</code>:</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Apply decay ranker to vector search</span>
result = milvus_client.search(
    collection_name,
    data=[<span class="hljs-string">&quot;music concerts&quot;</span>],              <span class="hljs-comment"># Query text</span>
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,                   <span class="hljs-comment"># Vector field to search</span>
    limit=<span class="hljs-number">10</span>,                             <span class="hljs-comment"># Number of results</span>
    output_fields=[<span class="hljs-string">&quot;title&quot;</span>, <span class="hljs-string">&quot;venue&quot;</span>, <span class="hljs-string">&quot;event_date&quot;</span>], <span class="hljs-comment"># Fields to return</span>
    ranker=ranker,                        <span class="hljs-comment"># Apply the decay ranker</span>
    consistency_level=<span class="hljs-string">&quot;Strong&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Aplicar a la búsqueda híbrida</h3><p>Los decay rankers también pueden aplicarse a operaciones de búsqueda híbrida que combinan múltiples campos vectoriales:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> AnnSearchRequest

<span class="hljs-comment"># Define dense vector search request</span>
dense = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;music concerts&quot;</span>],
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Define sparse vector search request</span>
sparse = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;music concerts&quot;</span>],
    anns_field=<span class="hljs-string">&quot;sparse_vector&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Apply decay ranker to hybrid search</span>
hybrid_results = milvus_client.hybrid_search(
    collection_name,
    [dense, sparse],                      <span class="hljs-comment"># Multiple search requests</span>
    ranker=ranker,                        <span class="hljs-comment"># Same decay ranker</span>
    limit=<span class="hljs-number">10</span>,
    output_fields=[<span class="hljs-string">&quot;title&quot;</span>, <span class="hljs-string">&quot;venue&quot;</span>, <span class="hljs-string">&quot;event_date&quot;</span>]
)
<button class="copy-code-btn"></button></code></pre>
<p>Para obtener más información sobre las operaciones de búsqueda híbrida, consulte <a href="/docs/es/multi-vector-search.md">Búsqueda híbrida multivectorial</a>.</p>
