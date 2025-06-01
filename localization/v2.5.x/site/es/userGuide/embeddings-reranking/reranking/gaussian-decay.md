---
id: gaussian-decay.md
title: Decaimiento gaussianoCompatible with Milvus 2.6.x
summary: >-
  El decaimiento gaussiano, también conocido como decaimiento normal, crea el
  ajuste más natural de los resultados de búsqueda. Al igual que la visión
  humana, que se difumina gradualmente con la distancia, el decaimiento
  gaussiano crea una curva suave en forma de campana que reduce suavemente la
  relevancia a medida que los elementos se alejan de su punto ideal. Este
  enfoque es ideal cuando se desea un decaimiento equilibrado que no penalice
  duramente los elementos que se encuentran justo fuera de su rango preferido,
  pero que reduzca significativamente la relevancia de los elementos distantes.
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">Decaimiento gaussiano<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>El decaimiento gaussiano, también conocido como decaimiento normal, crea el ajuste más natural de los resultados de búsqueda. Al igual que la visión humana, que se difumina gradualmente con la distancia, el decaimiento gaussiano crea una curva suave en forma de campana que reduce suavemente la relevancia a medida que los elementos se alejan de su punto ideal. Este enfoque es ideal cuando se desea un decaimiento equilibrado que no penalice duramente los elementos que se encuentran justo fuera del rango preferido, pero que reduzca significativamente la relevancia de los elementos distantes.</p>
<p>A diferencia de otros clasificadores:</p>
<ul>
<li><p>El decaimiento exponencial cae bruscamente al principio, creando una penalización inicial más fuerte.</p></li>
<li><p>El decaimiento lineal disminuye a un ritmo constante hasta llegar a cero, creando un límite claro.</p></li>
</ul>
<p>El decaimiento gaussiano proporciona un enfoque más equilibrado e intuitivo que resulta natural para los usuarios.</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">Cuándo utilizar el decaimiento gaussiano<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>El decaimiento gaussiano es especialmente eficaz para:</p>
<table>
   <tr>
     <th><p>Caso práctico</p></th>
     <th><p>Ejemplo</p></th>
     <th><p>Por qué funciona bien</p></th>
   </tr>
   <tr>
     <td><p>Búsquedas basadas en la ubicación</p></td>
     <td><p>Localizadores de restaurantes y tiendas</p></td>
     <td><p>Imita la percepción humana natural de la relevancia de la distancia</p></td>
   </tr>
   <tr>
     <td><p>Recomendaciones de contenido</p></td>
     <td><p>Sugerencias de artículos basadas en la fecha de publicación</p></td>
     <td><p>Disminución gradual de la relevancia a medida que el contenido envejece</p></td>
   </tr>
   <tr>
     <td><p>Listados de productos</p></td>
     <td><p>Artículos con precios cercanos al objetivo</p></td>
     <td><p>Disminución suave de la relevancia a medida que los precios se desvían del objetivo</p></td>
   </tr>
   <tr>
     <td><p>Búsqueda de expertos</p></td>
     <td><p>Búsqueda de profesionales con experiencia relevante</p></td>
     <td><p>Evaluación equilibrada de la relevancia de la experiencia</p></td>
   </tr>
</table>
<p>Si su aplicación requiere una sensación natural de disminución de la relevancia sin penalizaciones duras ni límites estrictos, el decaimiento gaussiano es probablemente su mejor opción.</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">Principio de la curva de Bell<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>El decaimiento gaussiano crea una curva suave en forma de campana que reduce gradualmente la relevancia a medida que aumenta la distancia desde un punto ideal. Esta distribución, que debe su nombre al matemático Carl Friedrich Gauss, aparece con frecuencia en la naturaleza y la estadística, lo que explica que resulte tan intuitiva para la percepción humana.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>Decaimiento gaussiano</span> </span></p>
<p>El gráfico anterior muestra cómo afectaría el decaimiento gaussiano a la clasificación de restaurantes en una aplicación de búsqueda móvil:</p>
<ul>
<li><p><code translate="no">origin</code> (0 km): Tu ubicación actual, donde la relevancia es máxima (1,0).</p></li>
<li><p><code translate="no">offset</code> (±300 m): La "zona de puntuación perfecta" que le rodea: todos los restaurantes situados a menos de 300 metros mantienen una puntuación de relevancia completa (1,0), lo que garantiza que las opciones más cercanas no se vean penalizadas innecesariamente por pequeñas diferencias de distancia.</p></li>
<li><p><code translate="no">scale</code> (±2 km): La distancia a la que la relevancia cae hasta el valor de decaimiento: los restaurantes situados a exactamente 2 kilómetros de distancia ven reducida a la mitad su puntuación de relevancia (0,5).</p></li>
<li><p><code translate="no">decay</code> (0.5): La puntuación a la distancia de escala: este parámetro controla esencialmente la rapidez con la que las puntuaciones disminuyen con la distancia.</p></li>
</ul>
<p>Como se puede ver en la curva, los restaurantes situados a más de 2 km siguen disminuyendo en relevancia, pero nunca llegan a cero. Incluso los restaurantes situados a 4-5 kilómetros conservan una relevancia mínima, lo que permite que restaurantes excelentes pero lejanos sigan apareciendo en los resultados (aunque con una clasificación inferior).</p>
<p>Este comportamiento imita la forma en que la gente piensa de forma natural sobre la relevancia de la distancia: se prefieren los lugares cercanos, pero estamos dispuestos a viajar más lejos para encontrar opciones excepcionales.</p>
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
    </button></h2><p>La fórmula matemática para calcular una puntuación de decaimiento gaussiano es:</p>
<p>$$ S(doc) = \exp\left( -\frac{\left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right)^2} {2\sigma^2} \right) $$</p>
<p>Donde:</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(decay)} $$</p>
<p>Desglosando esto en lenguaje sencillo:</p>
<ol>
<li><p>Calcular la distancia entre el valor de campo y el origen: $|fieldvalue_{doc} - origin|$</p></li>
<li><p>Restar el desplazamiento (si lo hay) pero nunca por debajo de cero: $\max(0, distancia - desplazamiento)$</p></li>
<li><p>Elevar al cuadrado esta distancia ajustada: $(distancia_ajustada)^2$</p></li>
<li><p>Dividir por $2\sigma^2$, que se calcula a partir de sus parámetros de escala y decaimiento</p></li>
<li><p>Tome el exponente negativo, que le da un valor entre 0 y 1: $\exp(-valor)$</p></li>
</ol>
<p>El cálculo de $\sigma^2$ convierte sus parámetros de escala y decaimiento en la desviación estándar al cuadrado de la distribución gaussiana. Esto es lo que da a la función su característica forma de campana.</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">Utilizar el decaimiento gaussiano<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>El decaimiento gaussiano puede aplicarse tanto a la búsqueda vectorial estándar como a las operaciones de búsqueda híbrida en Milvus. A continuación se muestran los fragmentos de código clave para implementar esta función.</p>
<div class="alert note">
<p>Antes de utilizar las funciones de decaimiento, primero debe crear una colección con los campos numéricos apropiados (como marcas de tiempo, distancias, etc.) que se utilizarán para los cálculos de decaimiento. Para ver ejemplos de trabajo completos que incluyan la configuración de la colección, la definición del esquema y la inserción de datos, consulte <a href="/docs/es/tutorial-implement-a-time-based-ranking-in-milvus.md">Tutorial: Implementar la clasificación basada en el tiempo en Milvus</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Crear un clasificador de decaimiento</h3><p>Después de configurar su colección con un campo numérico (en este ejemplo, <code translate="no">distance</code> en metros desde el usuario), cree un clasificador de decaimiento gaussiano:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Function, FunctionType

<span class="hljs-comment"># Create a Gaussian decay ranker for location-based restaurant search</span>
ranker = Function(
    name=<span class="hljs-string">&quot;restaurant_distance_decay&quot;</span>,     <span class="hljs-comment"># Function identifier</span>
    input_field_names=[<span class="hljs-string">&quot;distance&quot;</span>],       <span class="hljs-comment"># Numeric field for distance in meters</span>
    function_type=FunctionType.RERANK,    <span class="hljs-comment"># Function type. Must be RERANK</span>
    params={
        <span class="hljs-string">&quot;reranker&quot;</span>: <span class="hljs-string">&quot;decay&quot;</span>,              <span class="hljs-comment"># Specify decay reranker</span>
        <span class="hljs-string">&quot;function&quot;</span>: <span class="hljs-string">&quot;gauss&quot;</span>,              <span class="hljs-comment"># Choose Gaussian decay</span>
        <span class="hljs-string">&quot;origin&quot;</span>: <span class="hljs-number">0</span>,                      <span class="hljs-comment"># Your current location (0 meters)</span>
        <span class="hljs-string">&quot;offset&quot;</span>: <span class="hljs-number">300</span>,                    <span class="hljs-comment"># 300m no-decay zone</span>
        <span class="hljs-string">&quot;decay&quot;</span>: <span class="hljs-number">0.5</span>,                     <span class="hljs-comment"># Half score at scale distance</span>
        <span class="hljs-string">&quot;scale&quot;</span>: <span class="hljs-number">2000</span>                     <span class="hljs-comment"># 2 km scale (2000 meters)</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Aplicar a la búsqueda vectorial estándar</h3><p>Después de definir su decay ranker, puede aplicarlo durante las operaciones de búsqueda pasándolo al parámetro <code translate="no">ranker</code>:</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Apply decay ranker to restaurant vector search</span>
result = milvus_client.search(
    collection_name,
    data=[<span class="hljs-string">&quot;italian restaurants&quot;</span>],         <span class="hljs-comment"># Query text</span>
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,                   <span class="hljs-comment"># Vector field to search</span>
    limit=<span class="hljs-number">10</span>,                             <span class="hljs-comment"># Number of results</span>
    output_fields=[<span class="hljs-string">&quot;name&quot;</span>, <span class="hljs-string">&quot;cuisine&quot;</span>, <span class="hljs-string">&quot;distance&quot;</span>],  <span class="hljs-comment"># Fields to return</span>
    ranker=ranker,                        <span class="hljs-comment"># Apply the decay ranker</span>
    consistency_level=<span class="hljs-string">&quot;Strong&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Aplicar a la búsqueda híbrida</h3><p>Los decay rankers también pueden aplicarse a operaciones de búsqueda híbrida que combinan múltiples campos vectoriales:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> AnnSearchRequest

<span class="hljs-comment"># Define dense vector search request</span>
dense = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;italian restaurants&quot;</span>],
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Define sparse vector search request</span>
sparse = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;italian restaurants&quot;</span>],
    anns_field=<span class="hljs-string">&quot;sparse_vector&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Apply decay ranker to restaurant hybrid search</span>
hybrid_results = milvus_client.hybrid_search(
    collection_name,
    [dense, sparse],                      <span class="hljs-comment"># Multiple search requests</span>
    ranker=ranker,                        <span class="hljs-comment"># Same decay ranker</span>
    limit=<span class="hljs-number">10</span>,
    output_fields=[<span class="hljs-string">&quot;name&quot;</span>, <span class="hljs-string">&quot;cuisine&quot;</span>, <span class="hljs-string">&quot;distance&quot;</span>]
)
<button class="copy-code-btn"></button></code></pre>
<p>Para obtener más información sobre las operaciones de búsqueda híbrida, consulte <a href="/docs/es/multi-vector-search.md">Búsqueda híbrida multivectorial</a>.</p>
