---
id: gaussian-decay.md
title: Гауссово распадениеCompatible with Milvus 2.6.x
summary: >-
  Гауссово затухание, также известное как нормальное затухание, создает наиболее
  естественную корректировку результатов поиска. Подобно человеческому зрению,
  которое постепенно размывается с расстоянием, гауссово затухание создает
  плавную, колоколообразную кривую, которая плавно снижает релевантность по мере
  удаления элементов от вашей идеальной точки. Такой подход идеален, когда вам
  нужно сбалансированное затухание, которое не будет сильно наказывать объекты,
  находящиеся за пределами предпочтительного диапазона, но при этом значительно
  снизит релевантность удаленных объектов.
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">Гауссово распадение<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>Гауссово распадение, также известное как нормальное распадение, создает наиболее естественную корректировку результатов поиска. Подобно человеческому зрению, которое постепенно размывается с расстоянием, гауссово затухание создает плавную, колоколообразную кривую, которая плавно снижает релевантность по мере удаления объектов от вашей идеальной точки. Такой подход идеален, когда вам нужен сбалансированный распад, который не будет сильно наказывать объекты, находящиеся за пределами предпочтительного диапазона, но при этом значительно снизит релевантность удаленных объектов.</p>
<p>В отличие от других ранжировщиков распада:</p>
<ul>
<li><p>Экспоненциальный распад сначала резко снижается, создавая более сильное начальное наказание.</p></li>
<li><p>Линейный спад уменьшается с постоянной скоростью, пока не достигнет нуля, создавая четкую границу</p></li>
</ul>
<p>Гауссово распадение обеспечивает более сбалансированный, интуитивный подход, который кажется естественным для пользователей.</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">Когда использовать гауссово затухание<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>Гауссово затухание особенно эффективно для:</p>
<table>
   <tr>
     <th><p>Пример использования</p></th>
     <th><p>Пример</p></th>
     <th><p>Почему гауссово разложение хорошо работает</p></th>
   </tr>
   <tr>
     <td><p>Поиск по местоположению</p></td>
     <td><p>Поиск ресторанов, локаторы магазинов</p></td>
     <td><p>Имитирует естественное человеческое восприятие релевантности расстояния</p></td>
   </tr>
   <tr>
     <td><p>Рекомендации по содержанию</p></td>
     <td><p>Предложения статей на основе даты публикации</p></td>
     <td><p>Постепенное снижение релевантности по мере старения контента</p></td>
   </tr>
   <tr>
     <td><p>Объявления о товарах</p></td>
     <td><p>Товары, цены на которые близки к целевым</p></td>
     <td><p>Плавное снижение релевантности по мере отклонения цены от целевой</p></td>
   </tr>
   <tr>
     <td><p>Подбор специалистов</p></td>
     <td><p>Поиск профессионалов с соответствующим опытом</p></td>
     <td><p>Сбалансированная оценка релевантности опыта</p></td>
   </tr>
</table>
<p>Если вашему приложению требуется естественное ощущение снижения релевантности без жестких наказаний или строгих отсечек, то лучшим выбором будет гауссово затухание.</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">Принцип колоколообразной кривой<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>Гауссово затухание создает плавную, колоколообразную кривую, которая постепенно снижает релевантность по мере удаления от идеальной точки. Названное в честь математика Карла Фридриха Гаусса, это распределение часто встречается в природе и статистике, что объясняет, почему оно так интуитивно понятно для человеческого восприятия.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>Гауссово распадение</span> </span></p>
<p>На графике выше показано, как гауссово затухание повлияет на рейтинг ресторанов в мобильном поисковом приложении:</p>
<ul>
<li><p><code translate="no">origin</code> (0 км): Ваше текущее местоположение, где релевантность максимальна (1,0).</p></li>
<li><p><code translate="no">offset</code> (±300 m): "Зона идеальной оценки" вокруг вас - все рестораны в радиусе 300 метров сохраняют полную оценку релевантности (1,0), гарантируя, что очень близкие варианты не будут подвергаться ненужному наказанию за крошечную разницу в расстоянии.</p></li>
<li><p><code translate="no">scale</code> (±2 км): Расстояние, на котором релевантность снижается до значения распада - рестораны, расположенные на расстоянии ровно 2 км, получают вдвое меньше баллов релевантности (0,5).</p></li>
<li><p><code translate="no">decay</code> (0.5): Оценка на расстоянии шкалы - этот параметр, по сути, управляет тем, как быстро снижаются оценки с расстоянием.</p></li>
</ul>
<p>Как видно из кривой, рестораны, расположенные дальше 2 км, продолжают снижать свою релевантность, но так и не достигают нуля. Даже рестораны, расположенные на расстоянии 4-5 километров, сохраняют минимальную релевантность, что позволяет отличным, но удаленным ресторанам по-прежнему появляться в результатах (хотя и занимать более низкие места).</p>
<p>Такое поведение имитирует естественное восприятие людьми релевантности расстояния - близлежащие заведения предпочтительнее, но мы готовы отправиться дальше, чтобы получить исключительные варианты.</p>
<h2 id="Formula" class="common-anchor-header">Формула<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>Математическая формула для расчета показателя гауссова распада выглядит следующим образом:</p>
<p>$$ S(doc) = \exp\left( -\frac{\left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right)^2}{2\sigma^2} \right) $$</p>
<p>Где:</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(decay)} $$</p>
<p>Выражаясь простым языком:</p>
<ol>
<li><p>Вычислите, насколько далеко значение поля находится от начала координат: $|fieldvalue_{doc} - origin|$</p></li>
<li><p>Вычтите смещение (если оно есть), но никогда не опускайтесь ниже нуля: $\max(0, расстояние - смещение)$</p></li>
<li><p>Возведите в квадрат это скорректированное расстояние: $(скорректированное_расстояние)^2$</p></li>
<li><p>Разделите на $2\sigma^2$, которая рассчитывается из параметров масштаба и затухания.</p></li>
<li><p>Возьмите отрицательную экспоненту, которая дает значение между 0 и 1: $\exp(-value)$.</p></li>
</ol>
<p>Вычисление $\sigma^2$ преобразует ваши параметры масштаба и затухания в квадрат стандартного отклонения для гауссова распределения. Именно это придает функции характерную форму колокола.</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">Использование гауссова затухания<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>Гауссово затухание можно применять как к стандартному векторному поиску, так и к гибридным операциям поиска в Milvus. Ниже приведены ключевые фрагменты кода для реализации этой функции.</p>
<div class="alert note">
<p>Прежде чем использовать функции распада, необходимо создать коллекцию с соответствующими числовыми полями (например, временными метками, расстояниями и т. д.), которые будут использоваться для расчетов распада. Полные рабочие примеры, включающие настройку коллекции, определение схемы и вставку данных, см. в разделе <a href="/docs/ru/tutorial-implement-a-time-based-ranking-in-milvus.md">Учебник: Реализация ранжирования по времени в Milvus</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Создание ранжировщика распада</h3><p>После того как коллекция настроена с числовым полем (в данном примере <code translate="no">distance</code> в метрах от пользователя), создайте ранжировщик с гауссовым распадом:</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Применить к стандартному векторному поиску</h3><p>Определив ранжировщик распада, вы можете применить его во время поисковых операций, передав параметр <code translate="no">ranker</code>:</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Применить к гибридному поиску</h3><p>Ранжировщики распада также можно применять в гибридных поисковых операциях, которые объединяют несколько векторных полей:</p>
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
<p>Дополнительные сведения о гибридных операциях поиска см. в разделе <a href="/docs/ru/multi-vector-search.md">Многовекторный гибридный поиск</a>.</p>
