---
id: gaussian-decay.md
title: 高斯衰减Compatible with Milvus 2.6.x
summary: >-
  高斯衰减也称为正常衰减，它能对搜索结果进行最自然的调整。就像人的视力会随着距离的增加而逐渐模糊一样，高斯衰减会创建一条平滑的钟形曲线，随着项目远离您的理想点，相关性也会逐渐降低。这种方法非常适合您需要一种平衡的衰减方式，既不会对您偏好范围之外的项目造成严重影响，又能显著降低远处项目的相关性。
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">高斯衰减<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>高斯衰减也称为正常衰减，它能对搜索结果进行最自然的调整。就像人的视力会随着距离的增加而逐渐模糊一样，高斯衰减会创建一条平滑的钟形曲线，随着条目远离您的理想点，相关性会逐渐降低。这种方法非常适合您需要一种平衡的衰减方式，既不会对您偏好范围之外的项目造成严重影响，又能显著降低远处项目的相关性。</p>
<p>与其他衰减排名器不同：</p>
<ul>
<li><p>指数衰减一开始会急剧下降，从而产生较强的初始惩罚效果</p></li>
<li><p>线性衰减以恒定的速度递减，直至为零，形成一个清晰的分界线</p></li>
</ul>
<p>高斯衰减提供了一种更平衡、更直观的方法，让用户感觉很自然。</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">何时使用高斯衰减<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>高斯衰减对以下情况特别有效</p>
<table>
   <tr>
     <th><p>使用案例</p></th>
     <th><p>实例</p></th>
     <th><p>为什么高斯衰减效果好</p></th>
   </tr>
   <tr>
     <td><p>基于位置的搜索</p></td>
     <td><p>餐厅搜索器、商店定位器</p></td>
     <td><p>模仿人类对距离相关性的自然感知</p></td>
   </tr>
   <tr>
     <td><p>内容推荐</p></td>
     <td><p>基于出版日期的文章建议</p></td>
     <td><p>随着内容老化，相关性逐渐下降</p></td>
   </tr>
   <tr>
     <td><p>产品列表</p></td>
     <td><p>价格接近目标的商品</p></td>
     <td><p>价格偏离目标时相关性平稳下降</p></td>
   </tr>
   <tr>
     <td><p>专业知识匹配</p></td>
     <td><p>寻找具有相关经验的专业人士</p></td>
     <td><p>平衡评估经验相关性</p></td>
   </tr>
</table>
<p>如果您的应用需要相关性自然下降的感觉，而不需要严厉的惩罚或严格的截止条件，那么高斯衰减可能是您的最佳选择。</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">钟形曲线原理<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>高斯衰减会形成一条平滑的钟形曲线，随着与理想点的距离增加，相关性会逐渐降低。这种分布以数学家卡尔-弗里德里希-高斯（Carl Friedrich Gauss）的名字命名，经常出现在自然界和统计学中，这也解释了为什么人类对它有如此直观的感觉。</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>高斯衰减</span> </span></p>
<p>上图显示了高斯衰减如何影响移动搜索应用程序中的餐厅排名：</p>
<ul>
<li><p><code translate="no">origin</code> (0公里）：您的当前位置，相关性最大 (1.0)。</p></li>
<li><p><code translate="no">offset</code> (±300 m):您周围的 "满分区"--300 米内的所有餐厅都保持满分（1.0），确保附近的餐厅不会因为微小的距离差异而受到不必要的惩罚。</p></li>
<li><p><code translate="no">scale</code> (±2公里）：相关性下降到衰减值的距离--2 公里外的餐厅相关性得分减半（0.5）。</p></li>
<li><p><code translate="no">decay</code> (0.5):刻度距离上的分数--该参数主要控制分数随距离减小的速度。</p></li>
</ul>
<p>从曲线上可以看出，超过 2 公里的餐厅相关性会继续降低，但不会完全归零。即使是 4-5 公里以外的餐厅，也能保持最低限度的相关性，使优秀但距离较远的餐厅仍能出现在您的搜索结果中（尽管排名较低）。</p>
<p>这种行为模仿了人们对距离相关性的自然思维方式--附近的地方是首选，但我们愿意去更远的地方寻找特别的选择。</p>
<h2 id="Formula" class="common-anchor-header">计算公式<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>计算高斯衰减得分的数学公式为</p>
<p>S(doc) = exp\left( -frac{left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right)^2}{2\sigma^2}) $$\right) $$</p>
<p>其中</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(decay)} $$</p>
<p>用通俗易懂的语言将其分解：</p>
<ol>
<li><p>计算场值离原点的距离： $|fieldvalue_{doc} - origin|$</p></li>
<li><p>减去偏移量（如果有的话），但不要低于零： $\max(0, distance - offset)$</p></li>
<li><p>将调整后的距离平方： $(adjusted_distance)^2$</p></li>
<li><p>除以$2\sigma^2$，这是根据你的比例和衰减参数计算出来的</p></li>
<li><p>取负指数，得到一个介于 0 和 1 之间的值：$\exp(-value)$</p></li>
</ol>
<p>$\sigma^2$计算将规模和衰减参数转换为高斯分布的标准偏差平方。这就是赋予函数钟形特征的原因。</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">使用高斯衰减<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>高斯衰减可应用于 Milvus 中的标准向量搜索和混合搜索操作符。以下是实现这一功能的关键代码片段。</p>
<div class="alert note">
<p>在使用衰减函数之前，必须先创建一个带有适当数值字段（如时间戳、距离等）的 Collection，这些数值字段将用于衰减计算。有关包括集合设置、Schema 定义和数据插入在内的完整工作示例，请参阅<a href="/docs/zh/tutorial-implement-a-time-based-ranking-in-milvus.md">教程：在 Milvus 中实施基于时间的排名</a>。</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">创建衰减排名器</h3><p>用数字字段（在本例中，<code translate="no">distance</code> ，单位为距离用户的米）设置好 Collections 后，创建一个高斯衰减排序器：</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">应用于标准向量搜索</h3><p>定义好衰减排序器后，您就可以在搜索操作中将其应用到<code translate="no">ranker</code> 参数中：</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">应用于混合搜索</h3><p>衰减排序器还可以应用于结合多个向量场的混合搜索操作符：</p>
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
<p>有关混合搜索操作的更多信息，请参阅多<a href="/docs/zh/multi-vector-search.md">向量混合搜索</a>。</p>
