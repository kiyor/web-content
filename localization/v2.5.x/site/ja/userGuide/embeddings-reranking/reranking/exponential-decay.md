---
id: exponential-decay.md
title: 指数関数的減衰Compatible with Milvus 2.6.x
summary: >-
  指数関数的減衰は、検索結果にロングテールをもたらす。ニュース速報のように、最初は関連性が急速に低下するが、時間が経つにつれて重要性を保つストーリーもある。指数関数的減衰は、理想的な範囲を超えたアイテムに急激なペナルティを適用する一方で、遠くのアイテムは発見可能なままにしておく。このアプローチは、近接性や最新性を優先したいが、より遠い選択肢を完全に排除したくない場合に理想的である。
beta: Milvus 2.6.x
---
<h1 id="Exponential-Decay" class="common-anchor-header">指数関数的減衰<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Exponential-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>指数関数的減衰は、検索結果にロングテールをもたらす。ニュース速報のように、最初は関連性が急速に低下するが、時間が経つにつれて重要性を保つストーリーもあるように、指数関数的減衰は、理想的な範囲を超えたアイテムに急激なペナルティを適用する一方で、遠くのアイテムは発見可能なままにしておく。このアプローチは、近接性や最新性を優先したいが、より遠い選択肢を完全に排除したくない場合に理想的です。</p>
<p>他の減衰関数とは異なります：</p>
<ul>
<li><p>ガウス減衰は、より緩やかな、ベル型の減少を作成します。</p></li>
<li><p>線形減衰は、ちょうどゼロになるまで一定の割合で減少します。</p></li>
</ul>
<p>指数関数的減衰は、ペナルティをユニークに「フロントロード」し、レリバンスの減少の大部分を早期に適用する一方で、レリバンスは最小だがゼロではないロングテールを維持します。</p>
<h2 id="When-to-use-exponential-decay" class="common-anchor-header">指数減衰を使用するタイミング<button data-href="#When-to-use-exponential-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>指数減衰は以下のような場合に特に効果的です：</p>
<table>
   <tr>
     <th><p>使用例</p></th>
     <th><p>使用例</p></th>
     <th><p>指数関数が有効な理由</p></th>
   </tr>
   <tr>
     <td><p>ニュースフィード</p></td>
     <td><p>ニュースポータル</p></td>
     <td><p>数日前の重要なニュースを表示しながら、古いニュースの関連性を素早く下げることができます。</p></td>
   </tr>
   <tr>
     <td><p>ソーシャルメディアのタイムライン</p></td>
     <td><p>アクティビティフィード、ステータス更新</p></td>
     <td><p>新鮮なコンテンツに重点を置くが、バイラルな古いコンテンツも表示可能</p></td>
   </tr>
   <tr>
     <td><p>通知システム</p></td>
     <td><p>アラートの優先順位付け</p></td>
     <td><p>重要なアラートの可視性を維持しながら、最近のアラートに緊急性を持たせる。</p></td>
   </tr>
   <tr>
     <td><p>フラッシュセール</p></td>
     <td><p>期間限定オファー</p></td>
     <td><p>期限が近づくにつれ、視認性を急速に低下させる</p></td>
   </tr>
</table>
<p>次のような場合に指数関数的減衰を選択します：</p>
<ul>
<li><p>ユーザーは、ごく最近または近くのアイテムが検索結果を強く支配することを期待しています。</p></li>
<li><p>古いアイテムや遠いアイテムでも、特別に関連性が高ければ発見できるはずです。</p></li>
<li><p>関連性の落ち込みは前倒しで行う（最初は急で、後で緩やかになる）</p></li>
</ul>
<h2 id="Sharp-drop-off-principle" class="common-anchor-header">シャープドロップオフの原則<button data-href="#Sharp-drop-off-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>指数関数的減衰は、最初は急激に低下し、その後徐々に平坦になり、ゼロに近づくが決して到達しない長い尾を引く曲線を作る。この数学的パターンは、放射性物質の減衰、人口の減少、時間の経過に伴う情報の関連性などの自然現象に頻繁に現れる。</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/exp-decay.png" alt="Exp Decay" class="doc-image" id="exp-decay" />
   </span> <span class="img-wrapper"> <span>指数関数的減衰</span> </span></p>
<p>上のグラフは、指数関数的減衰がデジタルニュースプラットフォームにおけるニュース記事のランキングにどのような影響を与えるかを示している：</p>
<ul>
<li><p><code translate="no">origin</code> (現在時刻）：(現在時刻): 現在、関連性が最大(1.0)。</p></li>
<li><p><code translate="no">offset</code> (3時間）：過去3時間以内に発表された記事はすべて関連性スコアが満点（1.0）を維持し、ごく最近のニュースがわずかな時間差で不必要なペナルティを受けることはない。</p></li>
<li><p><code translate="no">decay</code> (0.5):このパラメータは、時間とともにスコアがどの程度劇的に減少するかをコントロールします。</p></li>
<li><p><code translate="no">scale</code> (24時間）：関連性が減衰値まで下がる時間-ちょうど24時間前のニュース記事は関連性スコアが半分（0.5）になる。</p></li>
</ul>
<p>曲線からわかるように、24時間以上前のニュース記事は関連性が下がり続けますが、ゼロになることはありません。数日前の記事でも最低限の関連性は保たれるため、重要だが古いニュースも（ランクは下がるものの）フィードに表示される。</p>
<p>この動作は、ニュースの関連性が一般的にどのように働くかを模倣しています。非常に最近のストーリーが強く支配的ですが、ユーザーの関心に特別に関連している場合、重要な古いストーリーがまだ突破できる可能性があります。</p>
<h2 id="Formula" class="common-anchor-header">計算式<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>指数減衰スコアを計算する数式は以下の通りです：</p>
<p>S(doc) = \expleft( ≖lambda ≖cdot ≖max ≖left(0, ≖left|fieldvalue_{doc} - originright ≖ offset ≖right)) $$ $</p>
<p>ここで</p>
<p>ここで、$$ \lambda = \frac{{ln(decay)}{scale} $$です。</p>
<p>これをわかりやすく分解すると</p>
<ol>
<li><p>フィールドの値が原点からどのくらい離れているかを計算します： $|fieldvalue_{doc} - origin|$.</p></li>
<li><p>もしあれば）オフセットを引くが、決してゼロ以下にはならない： $max(0, distance - offset)$.</p></li>
<li><p>スケールと減衰パラメータから計算される$lambda$を掛ける。</p></li>
<li><p>指数を取ると、0と1の間の値になる：$exp( \lambda Γcdot value)$.</p></li>
</ol>
<p>この$exp(exp(λ)Γcdot value)$は、スケールと減衰のパラメー タを指数関数のレートパラメータに変換する。より負の$lambda$は、より急な初期降下を作成する。</p>
<h2 id="Use-exponential-decay" class="common-anchor-header">指数減衰を使う<button data-href="#Use-exponential-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>指数関数的減衰はMilvusの標準的なベクトル探索とハイブリッド探索の両方に適用することができます。以下にこの機能を実装するための主要なコードスニペットを示します。</p>
<div class="alert note">
<p>減衰関数を使用する前に、まず減衰計算に使用する適切な数値フィールド（タイムスタンプ、距離など）を持つコレクションを作成する必要があります。コレクションのセットアップ、スキーマ定義、データ挿入を含む完全な作業例については、<a href="/docs/ja/tutorial-implement-a-time-based-ranking-in-milvus.md">ディケイランカーチュートリアルを</a>参照してください。</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">ディケイランカーの作成</h3><p>数値フィールド（この例では、<code translate="no">publish_time</code> ）でコレクションをセットアップした後、指数ディケイランカを作成します：</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">標準ベクトル検索に適用</h3><p>ディケイランカを定義した後、<code translate="no">ranker</code> パラメータに渡すことで、検索操作中に適用することができます：</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">ハイブリッド検索への適用</h3><p>ディケイランカーは複数のベクトルフィールドを組み合わせたハイブリッド検索操作にも適用できます：</p>
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
<p>ハイブリッド検索操作の詳細については、<a href="/docs/ja/multi-vector-search.md">マルチベクターハイブリッド検索を</a>参照してください。</p>
