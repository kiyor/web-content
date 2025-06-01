---
id: weighted-ranker.md
title: 가중랭커Compatible with Milvus 2.6.x
summary: >-
  가중랭커는 여러 검색 경로의 결과를 지능적으로 결합하고 각각에 서로 다른 중요도 가중치를 부여하여 우선순위를 정합니다. 숙련된 요리사가
  완벽한 요리를 만들기 위해 여러 재료의 균형을 맞추는 것처럼, 가중치 랭커는 서로 다른 검색 결과의 균형을 맞춰 가장 관련성이 높은 결과를
  조합합니다. 이 접근 방식은 특정 필드가 다른 필드보다 최종 순위에 더 크게 기여해야 하는 여러 벡터 필드 또는 양식에 걸쳐 검색할 때
  이상적입니다.
beta: Milvus 2.6.x
---
<h1 id="Weighted-Ranker" class="common-anchor-header">가중랭커<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h1><p>가중랭커는 여러 검색 경로의 결과를 지능적으로 결합하고 각각에 서로 다른 중요도 가중치를 부여하여 우선순위를 지정합니다. 숙련된 요리사가 완벽한 요리를 만들기 위해 여러 재료의 균형을 맞추는 것과 마찬가지로, 가중치 랭커는 서로 다른 검색 결과의 균형을 맞춰 가장 관련성이 높은 결과를 조합합니다. 이 접근 방식은 여러 벡터 필드 또는 양식에 걸쳐 검색할 때 특정 필드가 다른 필드보다 최종 순위에 더 크게 기여해야 하는 경우에 이상적입니다.</p>
<h2 id="When-to-use-Weighted-Ranker" class="common-anchor-header">가중치 랭커를 사용하는 경우<button data-href="#When-to-use-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>가중치 랭커는 여러 벡터 검색 경로의 결과를 결합해야 하는 하이브리드 검색 시나리오를 위해 특별히 설계되었습니다. 특히 다음과 같은 경우에 효과적입니다:</p>
<table>
   <tr>
     <th><p>사용 사례</p></th>
     <th><p>예시</p></th>
     <th><p>웨이트 랭커가 잘 작동하는 이유</p></th>
   </tr>
   <tr>
     <td><p>이커머스 검색</p></td>
     <td><p>이미지 유사도와 텍스트 설명을 결합한 제품 검색</p></td>
     <td><p>리테일러가 패션 상품의 경우 시각적 유사성을 우선시하는 동시에 기술 제품의 경우 텍스트 설명을 강조할 수 있습니다.</p></td>
   </tr>
   <tr>
     <td><p>미디어 콘텐츠 검색</p></td>
     <td><p>시각적 기능과 오디오 대본을 모두 사용한 비디오 검색</p></td>
     <td><p>쿼리 의도에 따라 시각적 콘텐츠와 음성 대화의 중요성 간의 균형을 맞출 수 있습니다.</p></td>
   </tr>
   <tr>
     <td><p>문서 검색</p></td>
     <td><p>다양한 섹션에 대한 여러 임베딩이 포함된 엔터프라이즈 문서 검색</p></td>
     <td><p>전체 텍스트 임베딩을 고려하면서 제목 및 초록 임베딩에 더 높은 가중치를 부여합니다.</p></td>
   </tr>
</table>
<p>하이브리드 검색 애플리케이션에서 여러 검색 경로를 결합하면서 상대적 중요도를 제어해야 하는 경우, 가중치 랭커가 이상적인 선택입니다.</p>
<h2 id="Mechanism-of-Weighted-Ranker" class="common-anchor-header">가중치 랭커의 메커니즘<button data-href="#Mechanism-of-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>웨이트 랭커 전략의 주요 워크플로는 다음과 같습니다:</p>
<ol>
<li><p><strong>검색 점수 수집</strong>: 벡터 검색의 각 경로(score_1, score_2)에서 결과와 점수를 수집합니다.</p></li>
<li><p><strong>점수 정규화</strong>: 각 검색은 서로 다른 유사성 메트릭을 사용할 수 있으므로 점수 분포가 달라질 수 있습니다. 예를 들어, 유사도 유형으로 내적 곱(IP)을 사용하면 [-∞,+∞] 범위의 점수가 나올 수 있는 반면, 유클리드 거리(L2)를 사용하면 [0,+∞] 범위의 점수가 나올 수 있습니다. 검색 방식에 따라 점수 범위가 다르고 직접 비교할 수 없으므로 각 검색 경로의 점수를 정규화해야 합니다. 일반적으로 <code translate="no">arctan</code> 함수를 적용하여 점수를 [0, 1] 사이의 범위로 변환합니다(score_1_normalized, score_2_normalized). 점수가 1에 가까울수록 유사성이 높음을 나타냅니다.</p></li>
<li><p><strong>가중치를 할당합니다</strong>: 서로 다른 벡터 필드에 할당된 중요도에 따라 가중치<strong>(wi)</strong>가 정규화된 점수(score_1_normalized, score_2_normalized)에 할당됩니다. 각 경로의 가중치는 [0,1] 범위여야 합니다. 결과 가중치 점수는 score_1_weighted 및 score_2_weighted입니다.</p></li>
<li><p><strong>점수 병합</strong>: 가중치 점수(score_1_weighted, score_2_weighted)를 가장 높은 점수부터 가장 낮은 점수까지 순위를 매겨 최종 점수 세트(score_final)를 생성합니다.</p></li>
</ol>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/weighted-ranker.png" alt="Weighted Ranker" class="doc-image" id="weighted-ranker" />
   </span> <span class="img-wrapper"> <span>가중 랭커</span> </span></p>
<h2 id="Example-of-Weighted-Ranker" class="common-anchor-header">가중 랭커의 예<button data-href="#Example-of-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>이 예는 이미지와 텍스트가 포함된 멀티모달 하이브리드 검색(topK=5)을 보여 주며, 가중치랭커 전략이 두 개의 ANN 검색 결과를 어떻게 재순위화하는지를 보여줍니다.</p>
<ul>
<li>이미지에 대한 ANN 검색 결과(topK=5): 다음과 같습니다.</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>점수(이미지)</strong></p></th>
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
<li>텍스트에 대한 ANN 검색 결과(topK=5)：： 다음과 같습니다.</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>점수(텍스트)</strong></p></th>
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
<li>가중치랭커를 사용하여 이미지 및 텍스트 검색 결과에 가중치를 할당합니다. 이미지 ANN 검색의 가중치는 0.6이고 텍스트 검색의 가중치는 0.4라고 가정합니다.</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>점수(이미지)</strong></p></th>
     <th><p><strong>점수(텍스트)</strong></p></th>
     <th><p><strong>가중치 점수</strong></p></th>
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
     <td><p>N/A</p></td>
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
     <td><p>이미지에 없음</p></td>
     <td><p>0.85</p></td>
     <td><p>0.6×0+0.4×0.85=0.34</p></td>
   </tr>
   <tr>
     <td><p>250</p></td>
     <td><p>이미지에 없음</p></td>
     <td><p>0.78</p></td>
     <td><p>0.6×0+0.4×0.78=0.312</p></td>
   </tr>
</table>
<ul>
<li>재랭크 후 최종 결과(상위 K=5): 다음과 같습니다.</li>
</ul>
<table>
   <tr>
     <th><p><strong>Rank</strong></p></th>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>최종 점수</strong></p></th>
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
<h2 id="Usage-of-Weighted-Ranker" class="common-anchor-header">가중 랭커 사용<button data-href="#Usage-of-Weighted-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>가중랭커 전략을 사용할 때는 가중치 값을 입력해야 합니다. 입력할 가중치 값의 개수는 하이브리드 검색의 기본 ANN 검색 요청 수와 일치해야 합니다. 입력 가중치 값은 [0,1] 범위에 속해야 하며, 1에 가까운 값일수록 중요도가 높음을 나타냅니다.</p>
<h3 id="Create-a-Weighted-Ranker" class="common-anchor-header">가중 랭킹 생성하기</h3><p>예를 들어, 하이브리드 검색에 텍스트 검색과 이미지 검색이라는 두 가지 기본 ANN 검색 요청이 있다고 가정해 보겠습니다. 텍스트 검색이 더 중요하다고 판단되면 더 큰 가중치를 할당해야 합니다.</p>
<div class="multipleCode">
   <a href="#python">파이썬</a> <a href="#java">자바</a> <a href="#go">Go</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">하이브리드 검색에 적용</h3><p>가중치 랭커는 여러 벡터 필드를 결합하는 하이브리드 검색 작업을 위해 특별히 설계되었습니다. 하이브리드 검색을 수행할 때는 각 검색 경로에 대한 가중치를 지정해야 합니다:</p>
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
<p>하이브리드 검색에 대한 자세한 내용은 <a href="/docs/ko/multi-vector-search.md">다중 벡터 하이브리드 검색을</a> 참조하세요.</p>
