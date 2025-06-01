---
id: exponential-decay.md
title: التضاؤل الأسيCompatible with Milvus 2.6.x
summary: >-
  يؤدي الاضمحلال الأسي إلى انخفاض أولي حاد يتبعه ذيل طويل في نتائج بحثك. مثل
  دورة الأخبار العاجلة حيث تتضاءل الأهمية بسرعة في البداية ولكن بعض القصص تحتفظ
  بأهميتها مع مرور الوقت، يطبق التضاؤل الأسي عقوبة حادة على العناصر التي تقع
  خارج النطاق المثالي مع الحفاظ على العناصر البعيدة قابلة للاكتشاف. هذا النهج
  مثالي عندما ترغب في إعطاء أولوية كبيرة للقرب أو التكرار ولكنك لا تريد استبعاد
  الخيارات البعيدة تمامًا.
beta: Milvus 2.6.x
---
<h1 id="Exponential-Decay" class="common-anchor-header">التضاؤل الأسي<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Exponential-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>يؤدي التضاؤل الأسي إلى انخفاض أولي حاد يتبعه ذيل طويل في نتائج بحثك. مثل دورة الأخبار العاجلة حيث تتضاءل الأهمية بسرعة في البداية ولكن بعض القصص تحتفظ بأهميتها مع مرور الوقت، يطبق التضاؤل الأسي عقوبة حادة على العناصر التي تقع خارج النطاق المثالي مع الحفاظ على العناصر البعيدة قابلة للاكتشاف. هذا النهج مثالي عندما ترغب في إعطاء الأولوية للقرب أو الحداثة بشكل كبير ولكنك لا تريد التخلص تمامًا من الخيارات البعيدة.</p>
<p>على عكس دوال الاضمحلال الأخرى:</p>
<ul>
<li><p>يخلق التضاؤل الغاوسي انخفاضًا تدريجيًا على شكل جرس</p></li>
<li><p>يتناقص التضاؤل الخطي بمعدل ثابت حتى يصل إلى الصفر تمامًا</p></li>
</ul>
<p>يعمل التضاؤل الأسي بشكل فريد على "تحميل العقوبة مقدمًا"، مما يؤدي إلى تطبيق معظم تخفيض الصلة في وقت مبكر مع الحفاظ على ذيل طويل من الصلة الدنيا ولكن غير الصفرية.</p>
<h2 id="When-to-use-exponential-decay" class="common-anchor-header">متى تستخدم التضاؤل الأسي<button data-href="#When-to-use-exponential-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>التضاؤل الأسي فعال بشكل خاص في:</p>
<table>
   <tr>
     <th><p>حالة الاستخدام</p></th>
     <th><p>مثال</p></th>
     <th><p>لماذا يعمل التضاؤل الأسي بشكل جيد</p></th>
   </tr>
   <tr>
     <td><p>موجز الأخبار</p></td>
     <td><p>بوابات الأخبار العاجلة</p></td>
     <td><p>يقلل بسرعة من أهمية الأخبار القديمة مع الاستمرار في عرض الأخبار المهمة من أيام مضت</p></td>
   </tr>
   <tr>
     <td><p>الجداول الزمنية لوسائل التواصل الاجتماعي</p></td>
     <td><p>موجزات النشاط وتحديثات الحالة</p></td>
     <td><p>يركز على المحتوى الجديد ولكنه يسمح بظهور المحتوى الأقدم سريع الانتشار</p></td>
   </tr>
   <tr>
     <td><p>أنظمة التنبيهات</p></td>
     <td><p>تحديد أولويات التنبيهات</p></td>
     <td><p>إنشاء تنبيهات عاجلة للتنبيهات الحديثة مع الحفاظ على وضوح التنبيهات المهمة</p></td>
   </tr>
   <tr>
     <td><p>التنزيلات السريعة</p></td>
     <td><p>العروض محدودة الوقت</p></td>
     <td><p>يقلل من الظهور بسرعة مع اقتراب الموعد النهائي</p></td>
   </tr>
</table>
<p>اختر التضاؤل الأسي عندما:</p>
<ul>
<li><p>يتوقع المستخدمون أن تهيمن العناصر الحديثة جدًا أو القريبة جدًا على النتائج بقوة</p></li>
<li><p>يجب أن تظل العناصر الأقدم أو البعيدة قابلة للاكتشاف إذا كانت ذات صلة بالموضوع بشكل استثنائي</p></li>
<li><p>يجب أن يكون الانخفاض في الصلة بالموضوع في المقدمة (أكثر حدة في البداية، وأكثر تدرجًا في وقت لاحق)</p></li>
</ul>
<h2 id="Sharp-drop-off-principle" class="common-anchor-header">مبدأ الانخفاض الحاد<button data-href="#Sharp-drop-off-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>ينشئ التضاؤل الأسي منحنى ينخفض بسرعة في البداية، ثم يتسطح تدريجياً إلى ذيل طويل يقترب من الصفر ولكنه لا يصل إلى الصفر أبداً. يظهر هذا النمط الرياضي بشكل متكرر في الظواهر الطبيعية مثل الاضمحلال الإشعاعي، وانخفاض عدد السكان، وأهمية المعلومات مع مرور الوقت.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/exp-decay.png" alt="Exp Decay" class="doc-image" id="exp-decay" />
   </span> <span class="img-wrapper"> <span>الاضمحلال الأسي</span> </span></p>
<p>يوضح الرسم البياني أعلاه كيف سيؤثر الاضمحلال الأسي على تصنيفات المقالات الإخبارية في منصة إخبارية رقمية:</p>
<ul>
<li><p><code translate="no">origin</code> (الوقت الحالي): اللحظة الحالية، حيث تكون الأهمية في أقصى درجاتها (1.0).</p></li>
<li><p><code translate="no">offset</code> (3 ساعات): "نافذة "الأخبار العاجلة" - جميع الأخبار المنشورة خلال الساعات الثلاث الأخيرة تحافظ على درجات الملاءمة الكاملة (1.0)، مما يضمن عدم معاقبة الأخبار الحديثة جدًا دون داعٍ بسبب الاختلافات الزمنية الطفيفة.</p></li>
<li><p><code translate="no">decay</code> (0.5): الدرجة في مسافة المقياس - يتحكم هذا المتغير في مدى انخفاض الدرجات بشكل كبير مع مرور الوقت.</p></li>
<li><p><code translate="no">scale</code> (24 ساعة): الفترة الزمنية التي تنخفض عندها الأهمية إلى قيمة الاضمحلال-المقالات الإخبارية التي مضى عليها 24 ساعة بالضبط تنخفض درجاتها إلى النصف (0.5).</p></li>
</ul>
<p>كما ترون من المنحنى، تستمر المقالات الإخبارية التي مضى عليها أكثر من 24 ساعة في الانخفاض في الأهمية ولكنها لا تصل إلى الصفر تمامًا. حتى القصص التي تعود إلى عدة أيام مضت تحتفظ بالحد الأدنى من الملاءمة، مما يسمح للأخبار المهمة ولكن الأقدم لا تزال تظهر في خلاصتك (وإن كان ترتيبها أقل).</p>
<p>يحاكي هذا السلوك كيفية عمل ملاءمة الأخبار عادةً - تهيمن القصص الحديثة جدًا بقوة، ولكن لا يزال بإمكان القصص الأقدم المهمة أن تبرز إذا كانت ذات صلة استثنائية باهتمامات المستخدم.</p>
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
    </button></h2><p>المعادلة الرياضية لحساب درجة التضاؤل الأسي هي</p>
<p>$$$ S(doc) = \ \ Exp\left( \ lambda \cdot \max \left(0, \left||||Fieldvalue_{doc} - الأصل \right|| - الإزاحة \right) \right) $$$$</p>
<p>حيث:</p>
<p>$$$ \lambda = \frac{\ln(decay)}{scale} $$$$</p>
<p>نحلل ذلك بلغة بسيطة</p>
<ol>
<li><p>احسب المسافة التي تبعد قيمة الحقل عن نقطة الأصل: |$$ قيمة الحقل \{دوك} - الأصل |$$.</p></li>
<li><p>اطرح الإزاحة (إن وجدت) ولكن لا تنخفض أبدًا إلى ما دون الصفر: \max (0$، المسافة - الإزاحة) \$.</p></li>
<li><p>اضرب في $ \lambda$، والذي يتم حسابه من معلمات المقياس والتضاؤل.</p></li>
<li><p>خذ الأس، والذي يعطيك قيمة بين 0 و1: $\ exp(\lambda \cdot value)$.</p></li>
</ol>
<p>يحول حساب \lambda$$ معاملات المقياس والتضاؤل إلى معلمة المعدل للدالة الأسية. تؤدي قيمة $\lambda$ الأكثر سالبة إلى انخفاض أولي أكثر حدة.</p>
<h2 id="Use-exponential-decay" class="common-anchor-header">استخدام التضاؤل الأسي<button data-href="#Use-exponential-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>يمكن تطبيق الاضمحلال الأسي على كل من عمليات البحث المتجه القياسية وعمليات البحث المختلطة في ميلفوس. فيما يلي مقتطفات الشيفرة الرئيسية لتطبيق هذه الميزة.</p>
<div class="alert note">
<p>قبل استخدام دوال التضاؤل، يجب عليك أولاً إنشاء مجموعة تحتوي على حقول رقمية مناسبة (مثل الطوابع الزمنية والمسافات وغيرها) والتي سيتم استخدامها لحسابات التضاؤل. للحصول على أمثلة عملية كاملة بما في ذلك إعداد المجموعة، وتعريف المخطط، وإدراج البيانات، راجع <a href="/docs/ar/tutorial-implement-a-time-based-ranking-in-milvus.md">البرنامج التعليمي لمصنف التضاؤل</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">إنشاء مصنف اضمحلال</h3><p>بعد إعداد المجموعة الخاصة بك مع حقل رقمي (في هذا المثال، <code translate="no">publish_time</code>)، قم بإنشاء مصنف تضاؤل أسي:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Function, FunctionType
<span class="hljs-keyword">import</span> datetime

<span class="hljs-comment"># Create an exponential decay ranker for news recency</span>
ranker = Function(
    name=<span class="hljs-string">&quot;news_recency&quot;</span>,                  <span class="hljs-comment"># Function identifier</span>
    input_field_names=[<span class="hljs-string">&quot;publish_time&quot;</span>],   <span class="hljs-comment"># Numeric field to use</span>
    function_type=FunctionType.RERANK,    <span class="hljs-comment"># Function type. Must be RERANK</span>
    params={
        <span class="hljs-string">&quot;reranker&quot;</span>: <span class="hljs-string">&quot;decay&quot;</span>,              <span class="hljs-comment"># Specify decay reranker</span>
        <span class="hljs-string">&quot;function&quot;</span>: <span class="hljs-string">&quot;exp&quot;</span>,                <span class="hljs-comment"># Choose exponential decay</span>
        <span class="hljs-string">&quot;origin&quot;</span>: <span class="hljs-built_in">int</span>(datetime.datetime.now().timestamp()),  <span class="hljs-comment"># Current time</span>
        <span class="hljs-string">&quot;offset&quot;</span>: <span class="hljs-number">3</span> * <span class="hljs-number">60</span> * <span class="hljs-number">60</span>,            <span class="hljs-comment"># 3 hour breaking news window</span>
        <span class="hljs-string">&quot;decay&quot;</span>: <span class="hljs-number">0.5</span>,                     <span class="hljs-comment"># Half score at scale distance</span>
        <span class="hljs-string">&quot;scale&quot;</span>: <span class="hljs-number">24</span> * <span class="hljs-number">60</span> * <span class="hljs-number">60</span>             <span class="hljs-comment"># 24 hours (1 day)</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">تطبيقه على البحث المتجه القياسي</h3><p>بعد تحديد مصنف التضاؤل الخاص بك، يمكنك تطبيقه أثناء عمليات البحث عن طريق تمريره إلى المعلمة <code translate="no">ranker</code>:</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Apply decay ranker to vector search</span>
result = milvus_client.search(
    collection_name,
    data=[<span class="hljs-string">&quot;market analysis&quot;</span>],             <span class="hljs-comment"># Query text</span>
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,                   <span class="hljs-comment"># Vector field to search</span>
    limit=<span class="hljs-number">10</span>,                             <span class="hljs-comment"># Number of results</span>
    output_fields=[<span class="hljs-string">&quot;title&quot;</span>, <span class="hljs-string">&quot;publish_time&quot;</span>], <span class="hljs-comment"># Fields to return</span>
    ranker=ranker,                        <span class="hljs-comment"># Apply the decay ranker</span>
    consistency_level=<span class="hljs-string">&quot;Strong&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">تطبيقه على البحث الهجين</h3><p>يمكن أيضًا تطبيق مصنفات التضاؤل على عمليات البحث المختلطة التي تجمع بين عدة حقول متجهة:</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> AnnSearchRequest

<span class="hljs-comment"># Define dense vector search request</span>
dense = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;market analysis&quot;</span>],
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Define sparse vector search request</span>
sparse = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;market analysis&quot;</span>],
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
    output_fields=[<span class="hljs-string">&quot;title&quot;</span>, <span class="hljs-string">&quot;publish_time&quot;</span>]
)
<button class="copy-code-btn"></button></code></pre>
<p>لمزيد من المعلومات حول عمليات البحث المختلط، راجع <a href="/docs/ar/multi-vector-search.md">البحث المختلط متعدد المتجهات</a>.</p>
