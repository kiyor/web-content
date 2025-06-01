---
id: gaussian-decay.md
title: ガウシアンディケイCompatible with Milvus 2.6.x
summary: >-
  通常の減衰としても知られるガウス減衰は、検索結果を最も自然な感じに調整します。距離によって徐々にぼやけていく人間の視覚のように、ガウシアン減衰は、アイテムが理想的なポイントから離れるにつれて、関連性が緩やかに減少する滑らかな釣鐘型の曲線を作成します。このアプローチは、希望の範囲外のアイテムに厳しいペナルティを与えることなく、それでも遠くのアイテムの関連性を大幅に下げる、バランスの取れた減衰を望む場合に理想的です。
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">ガウシアンディケイ<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>通常の減衰としても知られるガウス減衰は、検索結果を最も自然な感じに調整します。距離によって徐々にぼやけていく人間の視覚のように、ガウス減衰はアイテムが理想的なポイントから遠ざかるにつれて関連性が緩やかに減少する、滑らかな釣鐘型の曲線を作成します。このアプローチは、好みの範囲外のアイテムに厳しいペナルティを与えず、それでも遠くのアイテムの関連性を大幅に下げる、バランスの取れた減衰を望む場合に理想的です。</p>
<p>他のディケイランカーとは異なります：</p>
<ul>
<li><p>指数関数的減衰は、最初に急激に減少し、より強い初期ペナルティを生み出します。</p></li>
<li><p>線形減衰は、ゼロに達するまで一定の割合で減少し、明確なカットオフを作成します。</p></li>
</ul>
<p>ガウス減衰は、よりバランスの取れた直感的なアプローチを提供し、ユーザーにとって自然に感じられます。</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">ガウス減衰を使用する場合<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>ガウス減衰は特に以下のような場合に効果的です：</p>
<table>
   <tr>
     <th><p>使用例</p></th>
     <th><p>使用例</p></th>
     <th><p>ガウシアンが効果的な理由</p></th>
   </tr>
   <tr>
     <td><p>ロケーションベースの検索</p></td>
     <td><p>レストラン検索、店舗検索</p></td>
     <td><p>距離の関連性に関する人間の自然な知覚を模倣</p></td>
   </tr>
   <tr>
     <td><p>コンテンツ推薦</p></td>
     <td><p>出版日に基づく記事の提案</p></td>
     <td><p>コンテンツが古くなるにつれ、関連性が徐々に低下</p></td>
   </tr>
   <tr>
     <td><p>商品リスト</p></td>
     <td><p>ターゲットに近い価格の商品</p></td>
     <td><p>価格がターゲットから乖離するにつれて、関連性がスムーズに低下</p></td>
   </tr>
   <tr>
     <td><p>専門知識のマッチング</p></td>
     <td><p>関連する経験を持つ専門家の検索</p></td>
     <td><p>経験の関連性をバランスよく評価</p></td>
   </tr>
</table>
<p>厳しいペナルティや厳格なカットオフなしに、関連性が自然に低下していく感覚を必要とするアプリケーションには、ガウス減衰が最適です。</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">ベル曲線の原理<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>ガウス減衰は、理想的な点からの距離が長くなるにつれて関連性が徐々に低下する、滑らかなベル型の曲線を描きます。数学者カール・フリードリッヒ・ガウスにちなんで名付けられたこの分布は、自然界や統計学に頻繁に登場し、人間の知覚に直感的に感じられる理由の説明にもなっています。</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>ガウスの減衰</span> </span></p>
<p>上のグラフは、ガウス減衰がモバイル検索アプリのレストランランキングにどのような影響を与えるかを示している：</p>
<ul>
<li><p><code translate="no">origin</code> (0 km)：(0km)：現在地、関連性が最大(1.0)。</p></li>
<li><p><code translate="no">offset</code> (±300 m):(±300m)：あなたの周囲にある「満点ゾーン」。300m以内のレストランはすべて関連性の満点(1.0)を維持し、ごく近くの選択肢がわずかな距離の違いで不必要なペナルティを受けることはありません。</p></li>
<li><p><code translate="no">scale</code> (±2 km)：ちょうど2キロメートル離れたレストランは、関連性スコアが半分(0.5)になります。</p></li>
<li><p><code translate="no">decay</code> (0.5):スケール距離でのスコア-このパラメータは基本的に距離によってスコアがどの程度早く減少するかをコントロールする。</p></li>
</ul>
<p>曲線からわかるように、2キロを超えたレストランは関連性が下がり続けますが、ゼロになることはありません。4-5キロ離れたレストランでさえ、最低限の関連性を維持し、素晴らしいが遠いレストランが（ランクは低いものの）結果に表示されることを可能にしています。</p>
<p>この行動は、人々が距離の関連性について自然に考える方法を模倣しています-近くの場所が好まれますが、私たちは例外的なオプションのために遠くまで行くことをいとわないのです。</p>
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
    </button></h2><p>ガウス減衰スコアの計算式は以下の通りです：</p>
<p>$$
S(doc) = \exp\left( -\frac{\left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right)^2}{2\sigma^2}\right）$$とする。</p>
<p>ここで</p>
<p>ここで、$$ \sigma^2 = -frac{scale^2}{2 \cdot \ln(decay)}$です。</p>
<p>これをわかりやすく分解すると</p>
<ol>
<li><p>フィールドの値が原点からどのくらい離れているかを計算します。</p></li>
<li><p>オフセット（あれば）を引くが、ゼロ以下にはならない： $max(0, distance - offset)$</p></li>
<li><p>この調整距離を二乗する: $(adjusted_distance)^2$.</p></li>
<li><p>スケールと減衰パラメータから計算される$2sigma^2$で割る</p></li>
<li><p>負の指数を取ると、0と1の間の値が得られる： $exp(-value)$</p></li>
</ol>
<p>sigma^2$の計算は、スケールと減衰のパラメータをガウス分布の標準偏差の二乗に変換します。これは、関数に特徴的なベルの形を与えるものである。</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">ガウス減衰の使用<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>ガウス減衰はmilvusの標準的なベクトル探索とハイブリッド探索の両方に適用することができます。以下にこの機能を実装するための主要なコードスニペットを示します。</p>
<div class="alert note">
<p>減衰関数を使用する前に、まず減衰計算に使用する適切な数値フィールド（タイムスタンプ、距離など）を持つコレクションを作成する必要があります。コレクションのセットアップ、スキーマ定義、データ挿入を含む完全な作業例については、<a href="/docs/ja/tutorial-implement-a-time-based-ranking-in-milvus.md">チュートリアルを</a>参照してください<a href="/docs/ja/tutorial-implement-a-time-based-ranking-in-milvus.md">：Milvusでタイムベースランキングを実装するを</a>参照してください。</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">ディケイランカーの作成</h3><p>コレクションに数値フィールド（この例では、<code translate="no">distance</code> ユーザからのメートル単位）を設定したら、ガウス減衰ランカを作成します：</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">標準ベクトル検索に適用</h3><p>ディケイランカを定義した後、<code translate="no">ranker</code> パラメータに渡すことで、検索操作中に適用することができます：</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">ハイブリッド検索に適用</h3><p>ディケイランカーは複数のベクトル場を組み合わせたハイブリッド検索操作にも適用できます：</p>
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
<p>ハイブリッド検索操作の詳細については、<a href="/docs/ja/multi-vector-search.md">マルチベクターハイブリッド検索を</a>参照してください。</p>
