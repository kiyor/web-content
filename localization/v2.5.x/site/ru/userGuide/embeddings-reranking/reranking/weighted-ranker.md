---
id: weighted-ranker.md
title: Взвешенный ранжировщикCompatible with Milvus 2.6.x
summary: >-
  Weighted Ranker разумно комбинирует и приоритизирует результаты из нескольких
  путей поиска, присваивая каждому из них различные веса важности. Подобно тому,
  как опытный повар смешивает несколько ингредиентов для создания идеального
  блюда, Weighted Ranker уравновешивает различные результаты поиска для
  получения наиболее релевантных результатов. Такой подход идеален при поиске по
  нескольким векторным полям или модальностям, когда некоторые поля должны
  вносить более существенный вклад в итоговое ранжирование, чем другие.
beta: Milvus 2.6.x
---
<h1 id="Weighted-Ranker" class="common-anchor-header">Взвешенный ранжировщик<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h1><p>Weighted Ranker интеллектуально объединяет и приоритизирует результаты из нескольких путей поиска, присваивая каждому из них различные веса важности. Подобно тому, как опытный повар смешивает несколько ингредиентов для создания идеального блюда, Weighted Ranker уравновешивает различные результаты поиска для получения наиболее релевантных результатов. Такой подход идеален при поиске по нескольким векторным полям или модальностям, когда некоторые поля должны вносить более существенный вклад в итоговое ранжирование, чем другие.</p>
<h2 id="When-to-use-Weighted-Ranker" class="common-anchor-header">Когда использовать Weighted Ranker<button data-href="#When-to-use-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>Weighted Ranker специально разработан для гибридных сценариев поиска, в которых необходимо объединить результаты нескольких векторных путей поиска. Он особенно эффективен для:</p>
<table>
   <tr>
     <th><p>Пример использования</p></th>
     <th><p>Пример</p></th>
     <th><p>Почему взвешенный ранжировщик хорошо работает</p></th>
   </tr>
   <tr>
     <td><p>Поиск в электронной коммерции</p></td>
     <td><p>Поиск товаров, сочетающий сходство изображений и текстовых описаний</p></td>
     <td><p>Позволяет ритейлерам отдавать предпочтение визуальному сходству для модных товаров, в то время как текстовые описания для технических товаров имеют особое значение</p></td>
   </tr>
   <tr>
     <td><p>Поиск медиаконтента</p></td>
     <td><p>Поиск видео с использованием как визуальных характеристик, так и аудио-транскриптов</p></td>
     <td><p>Балансирует важность визуального контента по сравнению с разговорным диалогом на основе намерения запроса</p></td>
   </tr>
   <tr>
     <td><p>Поиск документов</p></td>
     <td><p>Корпоративный поиск документов с несколькими вложениями для различных разделов</p></td>
     <td><p>Придает больший вес вкраплениям заголовка и аннотации, но при этом учитывает полнотекстовые вкрапления</p></td>
   </tr>
</table>
<p>Если в вашем приложении для гибридного поиска требуется объединить несколько путей поиска, контролируя их относительную важность, Weighted Ranker - ваш идеальный выбор.</p>
<h2 id="Mechanism-of-Weighted-Ranker" class="common-anchor-header">Механизм работы Weighted Ranker<button data-href="#Mechanism-of-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>Основной рабочий процесс стратегии WeightedRanker выглядит следующим образом:</p>
<ol>
<li><p><strong>Сбор результатов поиска</strong>: Собираем результаты и баллы по каждому пути векторного поиска (score_1, score_2).</p></li>
<li><p><strong>Нормализация баллов</strong>: В каждом поиске могут использоваться различные метрики сходства, что приводит к различным распределениям баллов. Например, использование внутреннего продукта (IP) в качестве типа сходства может привести к оценкам в диапазоне [-∞,+∞], в то время как использование евклидова расстояния (L2) приводит к оценкам в диапазоне [0,+∞]. Поскольку диапазоны оценок при разных поисках отличаются и не могут быть напрямую сравнены, необходимо нормализовать оценки для каждого пути поиска. Обычно применяется функция <code translate="no">arctan</code> для преобразования оценок в диапазон между [0, 1] (score_1_normalized, score_2_normalized). Оценки, близкие к 1, указывают на большую схожесть.</p></li>
<li><p><strong>Присвоение весов</strong>: На основе важности, придаваемой различным векторным полям, нормализованным оценкам (score_1_normalized, score_2_normalized) присваиваются веса<strong>(wi</strong>). Веса каждого пути должны находиться в диапазоне [0,1]. Результирующими взвешенными оценками являются score_1_weighted и score_2_weighted.</p></li>
<li><p><strong>Слияние оценок</strong>: Взвешенные оценки (score_1_weighted, score_2_weighted) ранжируются от наибольшей к наименьшей, чтобы получить итоговый набор оценок (score_final).</p></li>
</ol>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/weighted-ranker.png" alt="Weighted Ranker" class="doc-image" id="weighted-ranker" />
   </span> <span class="img-wrapper"> <span>Взвешенный ранжировщик</span> </span></p>
<h2 id="Example-of-Weighted-Ranker" class="common-anchor-header">Пример взвешенного ранжировщика<button data-href="#Example-of-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>Этот пример демонстрирует мультимодальный гибридный поиск (topK=5) с использованием изображений и текста и показывает, как стратегия WeightedRanker ранжирует результаты двух ANN-поисков.</p>
<ul>
<li>Результаты поиска ANN по изображениям （topK=5)：：</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Оценка (изображение)</strong></p></th>
   </tr>
   <tr>
     <td><p>101</p></td>
     <td><p>0.92</p></td>
   </tr>
   <tr>
     <td><p>203</p></td>
     <td><p>0.88</p></td>
   </tr>
   <tr>
     <td><p>150</p></td>
     <td><p>0.85</p></td>
   </tr>
   <tr>
     <td><p>198</p></td>
     <td><p>0.83</p></td>
   </tr>
   <tr>
     <td><p>175</p></td>
     <td><p>0.8</p></td>
   </tr>
</table>
<ul>
<li>Результаты поиска ANN по текстам （topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Оценка (текст)</strong></p></th>
   </tr>
   <tr>
     <td><p>198</p></td>
     <td><p>0.91</p></td>
   </tr>
   <tr>
     <td><p>101</p></td>
     <td><p>0.87</p></td>
   </tr>
   <tr>
     <td><p>110</p></td>
     <td><p>0.85</p></td>
   </tr>
   <tr>
     <td><p>175</p></td>
     <td><p>0.82</p></td>
   </tr>
   <tr>
     <td><p>250</p></td>
     <td><p>0.78</p></td>
   </tr>
</table>
<ul>
<li>С помощью WeightedRanker присвойте веса результатам поиска изображений и текста. Предположим, что вес для поиска изображений ANN равен 0,6, а вес для поиска текста - 0,4.</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Оценка (изображение)</strong></p></th>
     <th><p><strong>Оценка (текст)</strong></p></th>
     <th><p><strong>Взвешенный балл</strong></p></th>
   </tr>
   <tr>
     <td><p>101</p></td>
     <td><p>0.92</p></td>
     <td><p>0.87</p></td>
     <td><p>0.6×0.92+0.4×0.87=0.90</p></td>
   </tr>
   <tr>
     <td><p>203</p></td>
     <td><p>0.88</p></td>
     <td><p>N/A</p></td>
     <td><p>0.6×0.88+0.4×0=0.528</p></td>
   </tr>
   <tr>
     <td><p>150</p></td>
     <td><p>0.85</p></td>
     <td><p>Н/Д</p></td>
     <td><p>0.6×0.85+0.4×0=0.51</p></td>
   </tr>
   <tr>
     <td><p>198</p></td>
     <td><p>0.83</p></td>
     <td><p>0.91</p></td>
     <td><p>0.6×0.83+0.4×0.91=0.86</p></td>
   </tr>
   <tr>
     <td><p>175</p></td>
     <td><p>0.80</p></td>
     <td><p>0.82</p></td>
     <td><p>0.6×0.80+0.4×0.82=0.81</p></td>
   </tr>
   <tr>
     <td><p>110</p></td>
     <td><p>Нет на изображении</p></td>
     <td><p>0.85</p></td>
     <td><p>0.6×0+0.4×0.85=0.34</p></td>
   </tr>
   <tr>
     <td><p>250</p></td>
     <td><p>Нет на изображении</p></td>
     <td><p>0.78</p></td>
     <td><p>0.6×0+0.4×0.78=0.312</p></td>
   </tr>
</table>
<ul>
<li>Итоговые результаты после повторного ранжирования（topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>Ранг</strong></p></th>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Итоговый балл</strong></p></th>
   </tr>
   <tr>
     <td><p>1</p></td>
     <td><p>101</p></td>
     <td><p>0.90</p></td>
   </tr>
   <tr>
     <td><p>2</p></td>
     <td><p>198</p></td>
     <td><p>0.86</p></td>
   </tr>
   <tr>
     <td><p>3</p></td>
     <td><p>175</p></td>
     <td><p>0.81</p></td>
   </tr>
   <tr>
     <td><p>4</p></td>
     <td><p>203</p></td>
     <td><p>0.528</p></td>
   </tr>
   <tr>
     <td><p>5</p></td>
     <td><p>150</p></td>
     <td><p>0.51</p></td>
   </tr>
</table>
<h2 id="Usage-of-Weighted-Ranker" class="common-anchor-header">Использование взвешенного ранжировщика<button data-href="#Usage-of-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>При использовании стратегии WeightedRanker необходимо ввести значения весов. Количество вводимых весовых значений должно соответствовать количеству базовых поисковых запросов ANN в гибридном поиске. Вводимые значения веса должны находиться в диапазоне [0,1], при этом значения ближе к 1 означают большую важность.</p>
<h3 id="Create-a-Weighted-Ranker" class="common-anchor-header">Создание взвешенного ранжировщика</h3><p>Например, предположим, что в гибридном поиске есть два основных поисковых запроса ANN: поиск текста и поиск изображений. Если текстовый поиск считается более важным, ему должен быть присвоен больший вес.</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#go">Go</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> WeightedRanker

<span class="hljs-comment"># Create a Weighted Ranker for multimodal search </span>
<span class="hljs-comment"># Weight for first search path (0.8) and second search path (0.3)</span>
rerank= WeightedRanker(<span class="hljs-number">0.8</span>, <span class="hljs-number">0.3</span>) 
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.ranker.WeightedRanker;

<span class="hljs-type">WeightedRanker</span> <span class="hljs-variable">rerank</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">WeightedRanker</span>(Arrays.asList(<span class="hljs-number">0.8f</span>, <span class="hljs-number">0.3f</span>))
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-go"><span class="hljs-keyword">import</span> <span class="hljs-string">&quot;github.com/milvus-io/milvus/client/v2/milvusclient&quot;</span>

reranker := milvusclient.NewWeightedReranker([]<span class="hljs-type">float64</span>{<span class="hljs-number">0.8</span>, <span class="hljs-number">0.3</span>})
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-attr">rerank</span>: <span class="hljs-title class_">WeightedRanker</span>(<span class="hljs-number">0.8</span>, <span class="hljs-number">0.3</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-built_in">export</span> rerank=<span class="hljs-string">&#x27;{
        &quot;strategy&quot;: &quot;ws&quot;,
        &quot;params&quot;: {&quot;weights&quot;: [0.8,0.3]}
    }&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Применение к гибридному поиску</h3><p>Weighted Ranker разработан специально для гибридного поиска, объединяющего несколько векторных полей. При выполнении гибридного поиска необходимо указать веса для каждого пути поиска:</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#javascript">NodeJS</a> <a href="#go">Go</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Python</span>
<span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> AnnSearchRequest

<span class="hljs-comment"># Define text vector search request</span>
text_search = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;modern dining table&quot;</span>],
    anns_field=<span class="hljs-string">&quot;text_vector&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Define image vector search request</span>
image_search = AnnSearchRequest(
    data=[image_embedding],  <span class="hljs-comment"># Image embedding vector</span>
    anns_field=<span class="hljs-string">&quot;image_vector&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Apply Weighted Ranker to product hybrid search</span>
<span class="hljs-comment"># Text search has 0.8 weight, image search has 0.3 weight</span>
hybrid_results = milvus_client.hybrid_search(
    collection_name,
    [text_search, image_search],  <span class="hljs-comment"># Multiple search requests</span>
    ranker=rerank,  <span class="hljs-comment"># Apply the weighted ranker</span>
    limit=<span class="hljs-number">10</span>,
    output_fields=[<span class="hljs-string">&quot;product_name&quot;</span>, <span class="hljs-string">&quot;price&quot;</span>, <span class="hljs-string">&quot;category&quot;</span>]
)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-comment">// java</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-comment">// nodejs</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-go"><span class="hljs-comment">// go</span>
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-comment"># restful</span>
<button class="copy-code-btn"></button></code></pre>
<p>Дополнительные сведения о гибридном поиске см. в разделе <a href="/docs/ru/multi-vector-search.md">Многовекторный гибридный поиск</a>.</p>
