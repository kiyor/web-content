---
id: gaussian-decay.md
title: 高斯衰減Compatible with Milvus 2.6.x
summary: >-
  高斯衰減 (Gaussian decay) 也稱為正常衰減 (normal
  decay)，會對搜尋結果進行最自然的調整。就像人類的視力會隨著距離逐漸模糊一樣，高斯遞減創造了一個平滑的鐘形曲線，當項目離您的理想點越遠時，相關性就會逐漸降低。當您想要一個平衡的衰減，既不會嚴重懲罰超出您偏好範圍的項目，又能顯著降低遠距離項目相關性的時候，這種方法是最理想的選擇。
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">高斯衰減<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>高斯衰減 (Gaussian Decay) 也稱為正常衰減 (normal decay)，會對搜尋結果進行最自然的調整。就像人類的視力會隨著距離逐漸模糊一樣，高斯遞減創造了一個平滑的鐘形曲線，當項目離您的理想點越遠時，相關性就會逐漸降低。當您想要一個平衡的衰減，既不會嚴重懲罰超出您偏好範圍的項目，又能顯著降低遙遠項目的相關性時，這種方法是最理想的選擇。</p>
<p>與其他衰減排名器不同：</p>
<ul>
<li><p>指數衰減一開始會急速下降，產生較強的初始懲罰。</p></li>
<li><p>線性衰減以固定速率遞減，直到達到零，創造一個明確的分界線</p></li>
</ul>
<p>高斯遞減提供了更平衡、更直觀的方法，讓使用者感覺自然。</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">何時使用高斯遞減<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>高斯衰減對以下情況特別有效</p>
<table>
   <tr>
     <th><p>使用個案</p></th>
     <th><p>範例</p></th>
     <th><p>為什麼高斯效果好</p></th>
   </tr>
   <tr>
     <td><p>基於位置的搜尋</p></td>
     <td><p>餐廳搜尋器、商店定位器</p></td>
     <td><p>模擬人類對距離相關性的自然感知</p></td>
   </tr>
   <tr>
     <td><p>內容推薦</p></td>
     <td><p>根據出版日期提供文章建議</p></td>
     <td><p>隨著內容老化，相關性逐漸下降</p></td>
   </tr>
   <tr>
     <td><p>產品清單</p></td>
     <td><p>價格接近目標的商品</p></td>
     <td><p>當價格偏離目標時，相關性平滑下降</p></td>
   </tr>
   <tr>
     <td><p>專業知識匹配</p></td>
     <td><p>尋找具有相關經驗的專業人士</p></td>
     <td><p>經驗相關性的平衡評估</p></td>
   </tr>
</table>
<p>如果您的應用程式需要相關性自然下降的感覺，而不需要嚴苛的懲罰或嚴格的截止值，高斯衰減可能是您的最佳選擇。</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">貝爾曲線原理<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>高斯衰減會產生平滑的鐘形曲線，隨著與理想點的距離增加，相關性也會逐漸降低。此分佈以數學家 Carl Friedrich Gauss 命名，經常出現在自然界和統計學中，這也解釋了為什麼人類對它的感覺如此直覺。</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>高斯衰減</span> </span></p>
<p>上圖顯示高斯衰減如何影響行動搜尋應用程式中的餐廳排名：</p>
<ul>
<li><p><code translate="no">origin</code> (0 km)：您目前的位置，相關性最高 (1.0)。</p></li>
<li><p><code translate="no">offset</code> (±300 m):您周圍的 「滿分區」-300 公尺內的所有餐廳都維持完整的相關性評分 (1.0)，確保附近的選項不會因為微小的距離差異而受到不必要的懲罰。</p></li>
<li><p><code translate="no">scale</code> (±2 公里)：相關度降至衰減值的距離 - 距離正好 2 公里的餐廳，其相關度分數會減半 (0.5)。</p></li>
<li><p><code translate="no">decay</code> (0.5):尺度距離上的分數-此參數基本上控制分數隨距離遞減的速度。</p></li>
</ul>
<p>從曲線可以看出，2 公里以外的餐廳相關度持續降低，但永遠不會達到零。即使是 4-5 公里外的餐廳，也會保留一些最低限度的相關性，讓優秀但距離較遠的餐廳仍然出現在您的結果中（儘管排名較低）。</p>
<p>這種行為模仿了人們對距離相關性的自然思考方式--鄰近的地方是首選，但我們願意為了特殊的選擇而走得更遠。</p>
<h2 id="Formula" class="common-anchor-header">計算公式<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>計算高斯衰減分數的數學公式如下：</p>
<p>$$ S(doc) = \exp\left( -\frac{left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right)^2}{2\sigma^2})\right) $$</p>
<p>其中：</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(decay)} $$</p>
<p>用簡單的語言分解：</p>
<ol>
<li><p>計算場值離原點的距離： $|fieldvalue_{doc} - origin|$</p></li>
<li><p>減去偏移量 (如果有的話)，但不要低於 0： $\max(0, distance - offset)$</p></li>
<li><p>將調整後的距離平方: $(adjusted_distance)^2$</p></li>
<li><p>除以 $2\sigma^2$，這是根據您的比例和衰減參數計算出來的。</p></li>
<li><p>取負指數，得到介於 0 和 1 之間的值：$\exp(-value)$</p></li>
</ol>
<p>$\sigma^2$ 計算將您的規模和衰減參數轉換為高斯分布的標準偏差平方。這就是賦予函數鐘形狀特徵的原因。</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">使用高斯衰減<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>在 Milvus 中，高斯衰減可應用於標準向量搜尋和混合搜尋運算。以下是實現此功能的關鍵程式碼片段。</p>
<div class="alert note">
<p>在使用衰減函數之前，您必須先建立一個具有適當數值欄位（如時間戳記、距離等）的集合，這些欄位將用於衰減計算。如需完整的工作範例，包括集合設定、模式定義和資料插入，請參閱<a href="/docs/zh-hant/tutorial-implement-a-time-based-ranking-in-milvus.md">教學：在 Milvus 中實施以時間為基礎的排名</a>。</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">建立衰減排名器</h3><p>在您的集合設定為數值欄位 (在本範例中，<code translate="no">distance</code> ，單位為距離使用者的公尺) 之後，建立一個高斯衰減排名器：</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">應用於標準向量搜尋</h3><p>定義衰減排序器之後，您可以將它傳給<code translate="no">ranker</code> 參數，在搜尋作業中應用它：</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">應用於混合搜尋</h3><p>衰減排序器也可以應用於結合多向量場的混合搜尋作業：</p>
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
<p>有關混合搜尋作業的詳細資訊，請參閱多<a href="/docs/zh-hant/multi-vector-search.md">向量混合搜尋</a>。</p>
