---
id: rrf-ranker.md
title: مصنف RRRFCompatible with Milvus 2.6.x
summary: >-
  مُصنّف دمج الرتب المتبادل (RRF) هو استراتيجية إعادة ترتيب للبحث الهجين Milvus
  الذي يوازن بين النتائج من مسارات بحث متعددة متجهة بناءً على مراكز ترتيبها
  بدلاً من درجات التشابه الخام. مثل البطولة الرياضية التي تأخذ في الاعتبار
  تصنيفات اللاعبين بدلاً من الإحصائيات الفردية، يجمع RRF Ranker بين نتائج البحث
  بناءً على مدى ارتفاع ترتيب كل عنصر في مسارات البحث المختلفة، مما يؤدي إلى
  إنشاء ترتيب نهائي عادل ومتوازن.
beta: Milvus 2.6.x
---
<h1 id="RRF-Ranker" class="common-anchor-header">مصنف RRRF<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h1><p>مصنف دمج الرتب المتبادل (RRF) هو استراتيجية إعادة ترتيب للبحث الهجين Milvus الذي يوازن بين النتائج من مسارات بحث متعددة المتجهات بناءً على مراكز ترتيبها بدلاً من درجات التشابه الخام. مثل البطولة الرياضية التي تأخذ في الاعتبار تصنيفات اللاعبين بدلاً من الإحصائيات الفردية، يقوم RRF Ranker بدمج نتائج البحث بناءً على مدى ارتفاع ترتيب كل عنصر في مسارات البحث المختلفة، مما يؤدي إلى إنشاء ترتيب نهائي عادل ومتوازن.</p>
<h2 id="When-to-use-RRF-Ranker" class="common-anchor-header">متى تستخدم مصنف RRF Ranker<button data-href="#When-to-use-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>تم تصميم RRF Ranker خصيصًا لسيناريوهات البحث المختلطة حيث تريد موازنة النتائج من مسارات بحث متعددة متجهة دون تعيين أوزان أهمية صريحة. إنه فعال بشكل خاص لـ</p>
<table>
   <tr>
     <th><p>حالة الاستخدام</p></th>
     <th><p>مثال</p></th>
     <th><p>لماذا يعمل مصنف RRF Ranker بشكل جيد</p></th>
   </tr>
   <tr>
     <td><p>البحث متعدد الوسائط بأهمية متساوية</p></td>
     <td><p>البحث عن الصور والنصوص حيث تكون كلتا الطريقتين متساويتين في الأهمية</p></td>
     <td><p>يوازن بين النتائج دون الحاجة إلى تعيينات وزن تعسفية</p></td>
   </tr>
   <tr>
     <td><p>بحث متجه التجميع</p></td>
     <td><p>الجمع بين النتائج من نماذج تضمين مختلفة</p></td>
     <td><p>يدمج التصنيفات بشكل ديمقراطي دون تفضيل توزيع درجات أي نموذج معين</p></td>
   </tr>
   <tr>
     <td><p>البحث عبر اللغات</p></td>
     <td><p>البحث عن المستندات عبر لغات متعددة</p></td>
     <td><p>ترتيب النتائج بشكل عادل بغض النظر عن خصائص التضمين الخاصة باللغة</p></td>
   </tr>
   <tr>
     <td><p>توصيات الخبراء</p></td>
     <td><p>الجمع بين التوصيات من أنظمة خبراء متعددة</p></td>
     <td><p>إنشاء تصنيفات توافقية عندما تستخدم أنظمة مختلفة أساليب تسجيل غير قابلة للمقارنة</p></td>
   </tr>
</table>
<p>إذا كان تطبيق البحث المختلط الخاص بك يتطلب موازنة مسارات بحث متعددة بشكل ديمقراطي دون تعيين أوزان صريحة، فإن RRF Ranker هو خيارك المثالي.</p>
<h2 id="Mechanism-of-RRF-Ranker" class="common-anchor-header">آلية مصنف RRF Ranker<button data-href="#Mechanism-of-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>سير العمل الرئيسي لاستراتيجية RRRFRanker على النحو التالي:</p>
<ol>
<li><p><strong>جمع تصنيفات البحث</strong>: اجمع تصنيفات النتائج من كل مسار من مسارات البحث المتجه (الرتبة_1، الرتبة_2).</p></li>
<li><p><strong>دمج التصنيفات</strong>: تحويل التصنيفات من كل مسار (rank_rf_1، rank_rf_rf_2) وفقًا لصيغة .</p>
<p>تتضمن الصيغة الحسابية <em>N،</em> والتي تمثل عدد عمليات الاسترجاع. <em>راندي</em><em>(د</em>) هو موضع ترتيب المستند <em>(د)</em> الناتج عن المسترجع <em>i(th)</em>. <em>k</em> هو معامل تنعيم يتم تعيينه عادةً عند 60.</p></li>
<li><p><strong>الترتيب الإجمالي</strong>: إعادة تصنيف نتائج البحث بناءً على التصنيفات المجمعة لإنتاج النتائج النهائية.</p></li>
</ol>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/rrf-ranker.png" alt="Rrf Ranker" class="doc-image" id="rrf-ranker" />
   </span> <span class="img-wrapper"> <span>مصنف RRRF</span> </span></p>
<h2 id="Example-of-RRF-Ranker" class="common-anchor-header">مثال على مصنف RRRF<button data-href="#Example-of-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>يوضح هذا المثال بحثًا هجينًا (topK=5) على متجهات متناثرة وكثيفة ويوضح كيفية إعادة ترتيب استراتيجية RRFR Ranker للنتائج من عمليتي بحث في الشبكة العصبية الاصطناعية.</p>
<ul>
<li>نتائج بحث ANN على متجهات متناثرة من النصوص （topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>المعرف</strong></p></th>
     <th><p><strong>الترتيب (متناثر)</strong></p></th>
   </tr>
   <tr>
     <td><p>101</p></td>
     <td><p>1</p></td>
   </tr>
   <tr>
     <td><p>203</p></td>
     <td><p>2</p></td>
   </tr>
   <tr>
     <td><p>150</p></td>
     <td><p>3</p></td>
   </tr>
   <tr>
     <td><p>198</p></td>
     <td><p>4</p></td>
   </tr>
   <tr>
     <td><p>175</p></td>
     <td><p>5</p></td>
   </tr>
</table>
<ul>
<li>نتائج بحث الشبكة العصبية الاصطناعية على متجهات كثيفة من النصوص （topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>المعرف</strong></p></th>
     <th><p><strong>الرتبة (كثيفة)</strong></p></th>
   </tr>
   <tr>
     <td><p>198</p></td>
     <td><p>1</p></td>
   </tr>
   <tr>
     <td><p>101</p></td>
     <td><p>2</p></td>
   </tr>
   <tr>
     <td><p>110</p></td>
     <td><p>3</p></td>
   </tr>
   <tr>
     <td><p>175</p></td>
     <td><p>4</p></td>
   </tr>
   <tr>
     <td><p>250</p></td>
     <td><p>5</p></td>
   </tr>
</table>
<ul>
<li>استخدم RRF لإعادة ترتيب ترتيب مجموعتي نتائج البحث. افترض أن معلمة التنعيم <code translate="no">k</code> مضبوطة على 60.</li>
</ul>
<table>
   <tr>
     <th><p><strong>المعرف</strong></p></th>
     <th><p><strong>النتيجة (متناثرة)</strong></p></th>
     <th><p><strong>النتيجة (كثيفة)</strong></p></th>
     <th><p><strong>النتيجة النهائية</strong></p></th>
   </tr>
   <tr>
     <td><p>101</p></td>
     <td><p>1</p></td>
     <td><p>2</p></td>
     <td><p>1/(60+1)+1/(60+2) = 0.01639</p></td>
   </tr>
   <tr>
     <td><p>198</p></td>
     <td><p>4</p></td>
     <td><p>1</p></td>
     <td><p>1/(60+4)+1/(60+1) = 0.01593</p></td>
   </tr>
   <tr>
     <td><p>175</p></td>
     <td><p>5</p></td>
     <td><p>4</p></td>
     <td><p>1/(60+5)+1/(60+4) = 0.01554</p></td>
   </tr>
   <tr>
     <td><p>203</p></td>
     <td><p>2</p></td>
     <td><p>غير متاح</p></td>
     <td><p>1/(60+2) = 0.01613</p></td>
   </tr>
   <tr>
     <td><p>150</p></td>
     <td><p>3</p></td>
     <td><p>غير متاح</p></td>
     <td><p>1/(60+3) = 0.01587</p></td>
   </tr>
   <tr>
     <td><p>110</p></td>
     <td><p>غير متاح</p></td>
     <td><p>3</p></td>
     <td><p>1/(60+3) = 0.01587</p></td>
   </tr>
   <tr>
     <td><p>250</p></td>
     <td><p>غير متاح</p></td>
     <td><p>5</p></td>
     <td><p>1/(60+5) = 0.01554</p></td>
   </tr>
</table>
<ul>
<li>النتائج النهائية بعد إعادة الترتيب （توبك=5)：النتائج النهائية بعد إعادة الترتيب</li>
</ul>
<table>
   <tr>
     <th><p><strong>الرتبة</strong></p></th>
     <th><p><strong>المعرف</strong></p></th>
     <th><p><strong>النتيجة النهائية</strong></p></th>
   </tr>
   <tr>
     <td><p>1</p></td>
     <td><p>101</p></td>
     <td><p>0.01639</p></td>
   </tr>
   <tr>
     <td><p>2</p></td>
     <td><p>203</p></td>
     <td><p>0.01613</p></td>
   </tr>
   <tr>
     <td><p>3</p></td>
     <td><p>198</p></td>
     <td><p>0.01593</p></td>
   </tr>
   <tr>
     <td><p>4</p></td>
     <td><p>150</p></td>
     <td><p>0.01587</p></td>
   </tr>
   <tr>
     <td><p>5</p></td>
     <td><p>110</p></td>
     <td><p>0.01587</p></td>
   </tr>
</table>
<h2 id="Usage-of-RRF-Ranker" class="common-anchor-header">استخدام مصنف RRRF<button data-href="#Usage-of-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>عند استخدام إستراتيجية إعادة الترتيب RRF، تحتاج إلى تكوين المعلمة <code translate="no">k</code>. وهي معلمة تنعيم يمكن أن تغير بشكل فعال الأوزان النسبية للبحث في النص الكامل مقابل البحث المتجه. القيمة الافتراضية لهذه المعلمة هي 60، ويمكن ضبطها ضمن نطاق (0، 16384). يجب أن تكون القيمة أرقام فاصلة عائمة. القيمة الموصى بها هي بين [10، 100]. في حين أن <code translate="no">k=60</code> هو خيار شائع، إلا أن القيمة المثلى <code translate="no">k</code> يمكن أن تختلف بناءً على تطبيقاتك ومجموعات البيانات الخاصة بك. نوصي باختبار هذه المعلمة وتعديلها بناءً على حالة الاستخدام الخاصة بك لتحقيق أفضل أداء.</p>
<h3 id="Create-an-RRF-Ranker" class="common-anchor-header">إنشاء مصنف RRRF</h3><p>بعد إعداد المجموعة الخاصة بك مع حقول متجهات متعددة، قم بإنشاء مصنف RRF مع معلمة تنعيم مناسبة:</p>
<div class="multipleCode">
   <a href="#python">بايثون</a> <a href="#java">جافا جافا</a> <a href="#go">جو</a> <a href="#javascript">نودجيس</a> <a href="#bash">cURL</a></div>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> RRFRanker

ranker = RRFRanker(<span class="hljs-number">100</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-java"><span class="hljs-keyword">import</span> io.milvus.v2.service.vector.request.ranker.RRFRanker;

<span class="hljs-type">RRFRanker</span> <span class="hljs-variable">ranker</span> <span class="hljs-operator">=</span> <span class="hljs-keyword">new</span> <span class="hljs-title class_">RRFRanker</span>(<span class="hljs-number">100</span>);
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-go">ranker := milvusclient.NewRRFReranker().WithK(<span class="hljs-number">100</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-javascript"><span class="hljs-attr">ranker</span>: <span class="hljs-title class_">RRFRanker</span>(<span class="hljs-string">&quot;100&quot;</span>)
<button class="copy-code-btn"></button></code></pre>
<pre><code translate="no" class="language-bash"><span class="hljs-string">&quot;ranker&quot;</span>: {
    <span class="hljs-string">&quot;strategy&quot;</span>: <span class="hljs-string">&quot;rrf&quot;</span>,
    <span class="hljs-string">&quot;params&quot;</span>: {
        <span class="hljs-string">&quot;k&quot;</span>: 100
    }
}
<span class="hljs-built_in">export</span> ranker=<span class="hljs-string">&#x27;{
        &quot;strategy&quot;: &quot;rrf&quot;,
        &quot;params&quot;: {&quot;k&quot;: 100}
    }&#x27;</span>
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">تطبيقه على البحث الهجين</h3><p>صُمم RRF Ranker خصيصًا لعمليات البحث المختلطة التي تجمع بين حقول متجهة متعددة. إليك كيفية استخدامه في البحث الهجين:</p>
<div class="multipleCode">
   <a href="#python">بايثون</a> <a href="#java">جافا جافا</a> <a href="#javascript">NodeJS</a> <a href="#go">Go</a> <a href="#bash">cURL</a></div>
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

<span class="hljs-comment"># Apply RRF Ranker to product hybrid search</span>
<span class="hljs-comment"># The smoothing parameter k controls the balance</span>
hybrid_results = milvus_client.hybrid_search(
    collection_name,
    [text_search, image_search],  <span class="hljs-comment"># Multiple search requests</span>
    ranker=ranker,  <span class="hljs-comment"># Apply the RRF ranker</span>
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
<p>لمزيد من المعلومات عن البحث الهجين، راجع <a href="/docs/ar/multi-vector-search.md">البحث الهجين متعدد المتجهات</a>.</p>
