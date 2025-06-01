---
id: gaussian-decay.md
title: الاضمحلال الغاوسيCompatible with Milvus 2.6.x
summary: >-
  ينشئ الاضمحلال الغاوسي، المعروف أيضًا باسم الاضمحلال الطبيعي، التعديل الأكثر
  طبيعية لنتائج بحثك. مثل الرؤية البشرية التي تتلاشى تدريجيًا مع المسافة، يخلق
  التضاؤل الغاوسي منحنى سلسًا على شكل جرس يقلل بلطف من ملاءمة العناصر كلما
  ابتعدت العناصر عن نقطتك المثالية. هذا النهج مثالي عندما تريد اضمحلالًا
  متوازنًا لا يعاقب العناصر التي تقع خارج النطاق المفضل لديك بقسوة ولكنه يقلل
  بشكل كبير من أهمية العناصر البعيدة.
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">الاضمحلال الغاوسي<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>ينشئ التضاؤل الغاوسي، المعروف أيضًا باسم التضاؤل الطبيعي، التعديل الأكثر طبيعية لنتائج بحثك. على غرار الرؤية البشرية التي تتلاشى تدريجيًا مع المسافة، يخلق التضاؤل الغاوسي منحنى سلسًا على شكل جرس يقلل بلطف من ملاءمة العناصر كلما ابتعدت العناصر عن نقطتك المثالية. هذا النهج مثالي عندما تريد اضمحلالًا متوازنًا لا يعاقب العناصر التي تقع خارج نطاقك المفضل بقسوة ولكنه يقلل بشكل كبير من أهمية العناصر البعيدة.</p>
<p>على عكس تصنيفات الاضمحلال الأخرى:</p>
<ul>
<li><p>ينخفض التضاؤل الأسي بشكل حاد في البداية، مما يخلق عقوبة أولية أقوى</p></li>
<li><p>يتناقص التضاؤل الخطي بمعدل ثابت حتى يصل إلى الصفر، مما يخلق حدًا فاصلًا واضحًا</p></li>
</ul>
<p>يوفر الاضمحلال الغاوسي نهجًا أكثر توازنًا وبديهيةً يبدو طبيعيًا للمستخدمين.</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">متى تستخدم التضاؤل الغاوسي<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>يكون التضاؤل الغاوسي فعالاً بشكل خاص في:</p>
<table>
   <tr>
     <th><p>حالة الاستخدام</p></th>
     <th><p>مثال</p></th>
     <th><p>لماذا يعمل غاوسي بشكل جيد</p></th>
   </tr>
   <tr>
     <td><p>عمليات البحث المستندة إلى الموقع</p></td>
     <td><p>مكتشفات المطاعم، ومحددات مواقع المتاجر</p></td>
     <td><p>تحاكي الإدراك البشري الطبيعي لمدى ملاءمة المسافة</p></td>
   </tr>
   <tr>
     <td><p>توصيات المحتوى</p></td>
     <td><p>اقتراحات المقالات بناءً على تاريخ النشر</p></td>
     <td><p>انخفاض تدريجي في الأهمية مع تقادم المحتوى</p></td>
   </tr>
   <tr>
     <td><p>قوائم المنتجات</p></td>
     <td><p>العناصر ذات الأسعار القريبة من الهدف</p></td>
     <td><p>انخفاض سلس في الملاءمة مع انحراف الأسعار عن الهدف</p></td>
   </tr>
   <tr>
     <td><p>مطابقة الخبرة</p></td>
     <td><p>العثور على محترفين ذوي خبرة ذات صلة</p></td>
     <td><p>تقييم متوازن لأهمية الخبرة</p></td>
   </tr>
</table>
<p>إذا كان تطبيقك يتطلب شعوراً طبيعياً بانخفاض الملاءمة دون عقوبات قاسية أو تخفيضات صارمة، فمن المحتمل أن يكون انحسار غاوسي هو خيارك الأفضل.</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">مبدأ منحنى الجرس<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>يخلق انحسار غاوسي منحنى سلس على شكل جرس يقلل تدريجياً من الملاءمة مع زيادة المسافة من نقطة مثالية. سُمي هذا التوزيع على اسم عالم الرياضيات كارل فريدريك غاوس، ويظهر هذا التوزيع بشكل متكرر في الطبيعة والإحصائيات، وهو ما يفسر سبب شعوره بأنه بديهي جدًا بالنسبة للإدراك البشري.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>تضاؤل غاوس</span> </span></p>
<p>يوضح الرسم البياني أعلاه كيف سيؤثر تضاؤل غاوس على تصنيفات المطاعم في تطبيق بحث على الهاتف المحمول:</p>
<ul>
<li><p><code translate="no">origin</code> (0 كم): موقعك الحالي، حيث تكون الأهمية في أقصى حد لها (1.0).</p></li>
<li><p><code translate="no">offset</code> (±300 m): "منطقة الدرجة المثالية" حولك - جميع المطاعم في نطاق 300 متر تحافظ على درجات الملاءمة الكاملة (1.0)، مما يضمن عدم معاقبة الخيارات القريبة جدًا دون داعٍ بسبب الاختلافات الصغيرة في المسافة.</p></li>
<li><p><code translate="no">scale</code> (± 2 كم): المسافة التي تنخفض عندها الملاءمة إلى قيمة الاضمحلال - المطاعم التي تبعد 2 كيلومتر بالضبط تنخفض درجات الملاءمة إلى النصف (0.5).</p></li>
<li><p><code translate="no">decay</code> (0.5): الدرجة عند مسافة المقياس - يتحكم هذا البارامتر بشكل أساسي في مدى سرعة تناقص الدرجات مع المسافة.</p></li>
</ul>
<p>كما ترى من المنحنى، تستمر المطاعم التي تبعد أكثر من 2 كم في الانخفاض في الأهمية ولكنها لا تصل إلى الصفر تمامًا. حتى المطاعم التي تبعد 4 إلى 5 كيلومترات تحتفظ بالحد الأدنى من الأهمية، مما يسمح للمطاعم الممتازة ولكن البعيدة بالظهور في نتائجك (وإن كان ترتيبها أقل).</p>
<p>هذا السلوك يحاكي كيف يفكر الناس بشكل طبيعي في مدى ملاءمة المسافة - فالأماكن القريبة مفضلة لدينا، ولكننا على استعداد للسفر لمسافة أبعد للحصول على خيارات استثنائية.</p>
<h2 id="Formula" class="common-anchor-header">المعادلة<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>الصيغة الرياضية لحساب درجة اضمحلال غاوسي هي</p>
<p>$$$$ S(doc) = \\xexp\left( - \frac{\left( \max \left(0, \left \left \||fieldvalue_{doc} - الأصل \right|| - الإزاحة \right) \right) \right)^2}{2\sigma^2} \يمين) $$$$</p>
<p>حيث:</p>
<p>$$$ \سيجما ^2 = - \frac{scale^2}{2 \cdot \ln(decay)} $$$$</p>
<p>نحلل ذلك بلغة بسيطة</p>
<ol>
<li><p>احسب المسافة التي تبعد قيمة الحقل عن نقطة الأصل: |$$ قيمة الحقل_{دوك} - الأصل |$</p></li>
<li><p>اطرح الإزاحة (إن وجدت) ولكن لا تنخفض أبدًا إلى ما دون الصفر: $\ماكس (0، المسافة - الإزاحة)$</p></li>
<li><p>قم بتربيع هذه المسافة المعدلة: $(المسافة_المعدلة)^2$</p></li>
<li><p>اقسم على 2 \سيجما ^2$، والتي يتم حسابها من معاملات المقياس والتضاؤل</p></li>
<li><p>خذ الأس السالب، وهو ما يمنحك قيمة بين 0 و1: $\sigma^2$ (-قيمة)$</p></li>
</ol>
<p>تحوّل عملية حساب $\سيجما ^2$ معاملات المقياس والتضاؤل إلى مربع الانحراف المعياري للتوزيع الغاوسي. هذا ما يعطي الدالة شكل الجرس المميز لها.</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">استخدام الاضمحلال الغاوسي<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>يمكن تطبيق الاضمحلال الغاوسي على كل من عمليات البحث المتجه القياسية وعمليات البحث المختلطة في ميلفوس. فيما يلي مقتطفات التعليمات البرمجية الرئيسية لتنفيذ هذه الميزة.</p>
<div class="alert note">
<p>قبل استخدام دوال الاضمحلال، يجب عليك أولاً إنشاء مجموعة تحتوي على حقول رقمية مناسبة (مثل الطوابع الزمنية والمسافات وغيرها) والتي سيتم استخدامها لحسابات الاضمحلال. للحصول على أمثلة عملية كاملة بما في ذلك إعداد المجموعة وتعريف المخطط وإدراج البيانات، راجع <a href="/docs/ar/tutorial-implement-a-time-based-ranking-in-milvus.md">البرنامج التعليمي: تنفيذ الترتيب المستند إلى الوقت في ميلفوس</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">إنشاء مصنف اضمحلال</h3><p>بعد إعداد المجموعة الخاصة بك مع حقل رقمي (في هذا المثال، <code translate="no">distance</code> بالأمتار من المستخدم)، قم بإنشاء مصنف اضمحلال غاوسي:</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">تطبيقه على البحث المتجه القياسي</h3><p>بعد تحديد مصنف الاضمحلال الخاص بك، يمكنك تطبيقه أثناء عمليات البحث عن طريق تمريره إلى المعلمة <code translate="no">ranker</code>:</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">تطبيقه على البحث الهجين</h3><p>يمكن أيضًا تطبيق مصنفات الاضمحلال على عمليات البحث المختلطة التي تجمع بين حقول متجهات متعددة:</p>
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
<p>لمزيد من المعلومات حول عمليات البحث المختلط، راجع <a href="/docs/ar/multi-vector-search.md">البحث المختلط متعدد المتجهات</a>.</p>
