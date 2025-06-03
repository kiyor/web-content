---
id: ivf-rabitq.md
title: IVF_RABITQ
summary: >-
  The IVF_RABITQ index is a binary quantization-based indexing algorithm that
  quantizes FP32 vectors into binary representations. It provides a highly
  configurable compression ratio with optional refinement for improved recall
  rates, making it suitable for applications requiring significant storage
  optimization.
beta: Milvus 2.6.x
---
<h1 id="IVFRABITQ" class="common-anchor-header">IVF_RABITQ<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#IVFRABITQ" class="anchor-icon" translate="no">
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
    </button></h1><p>The <strong>IVF_RABITQ</strong> index is a <strong>binary quantization-based</strong> indexing algorithm that quantizes FP32 vectors into binary representations. This index offers exceptional storage efficiency with a 1-to-32 compression ratio while maintaining relatively good recall rates. It supports optional refinement to achieve higher recall at the cost of additional storage, making it a versatile replacement for <a href="/docs/ivf-sq8.md">IVF_SQ8</a> and <a href="/docs/ivf-flat.md">IVF_FLAT</a> in memory-constrained scenarios.</p>
<h2 id="Overview" class="common-anchor-header">Overview<button data-href="#Overview" class="anchor-icon" translate="no">
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
    </button></h2><p>The <strong>IVF_RABITQ</strong> stands for <strong>Inverted File with RaBitQ quantization</strong>, combining two powerful techniques for efficient vector search and storage.</p>
<h3 id="IVF" class="common-anchor-header">IVF</h3><p><strong>Inverted File (IVF)</strong> organizes the vector space into manageable regions using <a href="https://en.wikipedia.org/wiki/K-means_clustering">k-means clustering</a>. Each cluster is represented by a centroid, serving as a reference point for the vectors within that cluster. This clustering approach reduces the search space by allowing the algorithm to focus only on the most relevant clusters during query processing.</p>
<p>To learn more about IVF technical details, refer to <a href="/docs/ivf-flat.md">IVF_FLAT</a>.</p>
<h3 id="RaBitQ" class="common-anchor-header">RaBitQ</h3><p><strong>RaBitQ</strong> is a state-of-the-art binary quantization method with theoretical guarantees, introduced in the research paper “RaBitQ: Quantizing High-Dimensional Vectors with a Theoretical Error Bound for Approximate Nearest Neighbor Search” by Jianyang Gao and Cheng Long.</p>
<p>RaBitQ introduces several innovative concepts:</p>
<p><strong>Angular Information Encoding</strong>: Unlike traditional spatial encoding, RaBitQ encodes angular information through vector normalization. In IVF_RABITQ, data vectors are normalized against their nearest IVF centroid, enhancing the precision of the quantization process.</p>
<p><strong>Theoretical Foundation</strong>: The core distance approximation formula is:</p>
<p>$${\lVert}\bold{o_r}-\bold{q_r}{\rVert}^2 \approx {\lVert}\bold{o_r}-\bold{c_o}{\rVert}^2+{\lVert}\bold{q_r}-\bold{c_o}{\rVert}^2-2 \cdot C(\bold{o_r},\bold{c_o}) \cdot (\tilde{\bold{o}},\bold{q_r}-\bold{c_o}) + C_1(\bold{o_r},\bold{c_o})$$</p>
<p>Where:</p>
<ul>
<li>$\bold{o_r}$ is a data vector from the dataset</li>
<li>$\bold{q_r}$ is a query vector</li>
<li>$\bold{c_o}$ is the nearest IVF centroid vector for $\bold{o_r}$</li>
<li>$C(\bold{o_r},\bold{c_o})$ and $C_1(\bold{o_r},\bold{c_o})$ are precomputed constants</li>
<li>$\tilde{\bold{o}}$ is the quantized binary vector stored in the index</li>
<li>$(\tilde{\bold{o}},\bold{q_r}-\bold{c_o})$ represents the dot-product operation</li>
</ul>
<p><strong>Computational Efficiency</strong>: The binary nature of $\tilde{\bold{o}}$ makes distance calculations extremely fast, particularly benefiting from modern CPU architectures with dedicated <code translate="no">AVX512VPOPCNTDQ</code> instructions on Intel IceLake+ or AMD Zen 4+ processors.</p>
<p><strong>Algorithmic Enhancements</strong>: RaBitQ integrates effectively with established techniques like the <a href="https://www.vldb.org/pvldb/vol9/p288-andre.pdf"><code translate="no">FastScan</code> approach</a> and <a href="https://github.com/facebookresearch/faiss/wiki/Pre--and-post-processing">random rotations</a> for improved performance.</p>
<h3 id="IVF-+-RaBitQ" class="common-anchor-header">IVF + RaBitQ</h3><p>The <strong>IVF_RABITQ</strong> index combines IVF’s efficient clustering with RaBitQ’s advanced binary quantization:</p>
<ol>
<li><p><strong>Coarse Filtering</strong>: IVF partitions the vector space into clusters, significantly reducing the search scope by focusing on the most relevant cluster regions.</p></li>
<li><p><strong>Binary Quantization</strong>: Within each cluster, RaBitQ compresses vectors into binary representations while preserving essential distance relationships through theoretical guarantees.</p></li>
<li><p><strong>Optional Refinement</strong>: When enabled, the index stores additional refined data using higher precision formats (SQ6, SQ8, FP16, BF16, or FP32) to improve recall rates at the cost of increased storage.</p></li>
</ol>
<p>Milvus implements IVF_RABITQ using the following FAISS factory strings:</p>
<ul>
<li>With refinement: <code translate="no">&quot;RR({dim}),IVF{nlist},RaBitQ,Refine({refine_index})&quot;</code></li>
<li>Without refinement: <code translate="no">&quot;RR({dim}),IVF{nlist},RaBitQ&quot;</code></li>
</ul>
<h2 id="Build-index" class="common-anchor-header">Build index<button data-href="#Build-index" class="anchor-icon" translate="no">
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
    </button></h2><p>To build an <code translate="no">IVF_RABITQ</code> index on a vector field in Milvus, use the <code translate="no">add_index()</code> method, specifying the <code translate="no">index_type</code>, <code translate="no">metric_type</code>, and additional parameters for the index.</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> MilvusClient

<span class="hljs-comment"># Prepare index building params</span>
index_params = MilvusClient.prepare_index_params()

index_params.add_index(
    field_name=<span class="hljs-string">&quot;your_vector_field_name&quot;</span>, <span class="hljs-comment"># Name of the vector field to be indexed</span>
    index_type=<span class="hljs-string">&quot;IVF_RABITQ&quot;</span>, <span class="hljs-comment"># Type of the index to create</span>
    <span class="hljs-comment"># highlight-next-line</span>
    index_name=<span class="hljs-string">&quot;vector_index&quot;</span>, <span class="hljs-comment"># Name of the index to create</span>
    metric_type=<span class="hljs-string">&quot;L2&quot;</span>, <span class="hljs-comment"># Metric type used to measure similarity</span>
    <span class="hljs-comment"># highlight-start</span>
    params={
        <span class="hljs-string">&quot;nlist&quot;</span>: <span class="hljs-number">1024</span>, <span class="hljs-comment"># Number of clusters for the index</span>
        <span class="hljs-string">&quot;refine&quot;</span>: <span class="hljs-literal">True</span>, <span class="hljs-comment"># Enable refinement for higher recall</span>
        <span class="hljs-string">&quot;refine_type&quot;</span>: <span class="hljs-string">&quot;SQ8&quot;</span> <span class="hljs-comment"># Refinement data format</span>
    } <span class="hljs-comment"># Index building params</span>
    <span class="hljs-comment"># highlight-end</span>
)
<button class="copy-code-btn"></button></code></pre>
<p>In this configuration:</p>
<ul>
<li><p><code translate="no">index_type</code>: The type of index to be built. In this example, set the value to <code translate="no">IVF_RABITQ</code>.</p></li>
<li><p><code translate="no">metric_type</code>: The method used to calculate the distance between vectors. Supported values include <code translate="no">COSINE</code>, <code translate="no">L2</code>, and <code translate="no">IP</code>. For details, refer to <a href="/docs/metric.md">Metric Types</a>.</p></li>
<li><p><code translate="no">params</code>: Additional configuration options for building the index. For details, refer to <a href="/docs/ivf-rabitq.md#Index-building-params">Index building params</a>.</p></li>
</ul>
<p>Once the index parameters are configured, you can create the index by using the <code translate="no">create_index()</code> method directly or passing the index params in the <code translate="no">create_collection</code> method. For details, refer to <a href="/docs/create-collection.md">Create Collection</a>.</p>
<h2 id="Search-on-index" class="common-anchor-header">Search on index<button data-href="#Search-on-index" class="anchor-icon" translate="no">
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
    </button></h2><p>Once the index is built and entities are inserted, you can perform similarity searches on the index.</p>
<pre><code translate="no" class="language-python">search_params = {
    <span class="hljs-comment"># highlight-start</span>
    <span class="hljs-string">&quot;params&quot;</span>: {
        <span class="hljs-string">&quot;nprobe&quot;</span>: <span class="hljs-number">128</span>, <span class="hljs-comment"># Number of clusters to search</span>
        <span class="hljs-string">&quot;rbq_query_bits&quot;</span>: <span class="hljs-number">0</span>, <span class="hljs-comment"># Query vector quantization bits</span>
        <span class="hljs-string">&quot;refine_k&quot;</span>: <span class="hljs-number">1</span> <span class="hljs-comment"># Refinement magnification factor</span>
    }
    <span class="hljs-comment"># highlight-end</span>
}

res = MilvusClient.search(
    collection_name=<span class="hljs-string">&quot;your_collection_name&quot;</span>, <span class="hljs-comment"># Collection name</span>
    anns_field=<span class="hljs-string">&quot;vector_field&quot;</span>, <span class="hljs-comment"># Vector field name</span>
    data=[[<span class="hljs-number">0.1</span>, <span class="hljs-number">0.2</span>, <span class="hljs-number">0.3</span>, <span class="hljs-number">0.4</span>, <span class="hljs-number">0.5</span>]], <span class="hljs-comment"># Query vector</span>
    limit=<span class="hljs-number">3</span>, <span class="hljs-comment"># TopK results to return</span>
    <span class="hljs-comment"># highlight-next-line</span>
    search_params=search_params
)
<button class="copy-code-btn"></button></code></pre>
<p>In this configuration:</p>
<ul>
<li><code translate="no">params</code>: Additional configuration options for searching on the index. For details, refer to <a href="/docs/ivf-rabitq.md#Index-specific-search-params">Index-specific search params</a>.</li>
</ul>
<div class="alert note">
<p>The IVF_RABITQ index heavily relies on the <code translate="no">popcount</code> hardware instruction for optimal performance. Modern CPU architectures such as Intel IceLake+ or AMD Zen 4+ with <code translate="no">AVX512VPOPCNTDQ</code> instruction sets provide significant performance improvements for RaBitQ operations.</p>
</div>
<h2 id="Index-params" class="common-anchor-header">Index params<button data-href="#Index-params" class="anchor-icon" translate="no">
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
    </button></h2><p>This section provides an overview of the parameters used for building an index and performing searches on the index.</p>
<h3 id="Index-building-params" class="common-anchor-header">Index building params</h3><p>The following table lists the parameters that can be configured in <code translate="no">params</code> when <a href="/docs/ivf-rabitq.md#Build-index">building an index</a>.</p>
<table>
   <tr>
     <th></th>
     <th><p>Parameter</p></th>
     <th><p>Description</p></th>
     <th><p>Value Range</p></th>
     <th><p>Tuning Suggestion</p></th>
   </tr>
   <tr>
     <td><p>IVF</p></td>
     <td><p><code translate="no">nlist</code></p></td>
     <td><p>The number of clusters to create using the k-means algorithm during index building. Each cluster, represented by a centroid, stores a list of vectors. Increasing this parameter reduces the number of vectors in each cluster, creating smaller, more focused partitions.</p></td>
     <td><p><strong>Type</strong>: Integer<br><strong>Range</strong>: [1, 65536]<br><strong>Default value</strong>: <code translate="no">128</code></p></td>
     <td><p>Larger <code translate="no">nlist</code> values improve recall by creating more refined clusters but increase index building time. Optimize based on dataset size and available resources. In most cases, we recommend you set a value within this range: [32, 4096].</p></td>
   </tr>
   <tr>
     <td rowspan="3"><p>RaBitQ</p></td>
     <td><p><code translate="no">refine</code></p></td>
     <td><p>Enables the refine process and stores the refined data.</p></td>
     <td><p><strong>Type</strong>: Boolean<br><strong>Range</strong>: [<code translate="no">true</code>, <code translate="no">false</code>]<br><strong>Default value</strong>: <code translate="no">false</code></p></td>
     <td><p>Set to <code translate="no">true</code> if a 0.9+ recall rate is needed. Enabling refinement improves accuracy but increases storage requirements and index building time.</p></td>
   </tr>
   <tr>
     <td><p><code translate="no">refine_type</code></p></td>
     <td><p>Defines the data representation used for refining when <code translate="no">refine</code> is enabled.</p></td>
     <td><p><strong>Type</strong>: String<br><strong>Range</strong>: [<code translate="no">SQ6</code>, <code translate="no">SQ8</code>, <code translate="no">FP16</code>, <code translate="no">BF16</code>, <code translate="no">FP32</code>]<br><strong>Default value</strong>: None</p></td>
     <td><p>The listed values are presented in order of increasing recall rate, decreasing QPS, and increasing storage size. <code translate="no">SQ8</code> is recommended as a starting point, offering a good balance between accuracy and resource usage.</p></td>
   </tr>
</table>
<h3 id="Index-specific-search-params" class="common-anchor-header">Index-specific search params</h3><p>The following table lists the parameters that can be configured in <code translate="no">search_params.params</code> when <a href="/docs/ivf-rabitq.md#Search-on-index">searching on the index</a>.</p>
<table>
   <tr>
     <th></th>
     <th><p>Parameter</p></th>
     <th><p>Description</p></th>
     <th><p>Value Range</p></th>
     <th><p>Tuning Suggestion</p></th>
   </tr>
   <tr>
     <td><p>IVF</p></td>
     <td><p><code translate="no">nprobe</code></p></td>
     <td><p>The number of clusters to search for candidates. Higher values allow more clusters to be searched, improving recall by expanding the search scope but at the cost of increased query latency.</p></td>
     <td><p><strong>Type</strong>: Integer<br><strong>Range</strong>: [1, <em>nlist</em>]<br><strong>Default value</strong>: <code translate="no">8</code></p></td>
     <td><p>Increasing this value improves recall but may slow down the search. Set <code translate="no">nprobe</code> proportionally to <code translate="no">nlist</code> to balance speed and accuracy. In most cases, we recommend you set a value within this range: [1, <em>nlist</em>].</p></td>
   </tr>
   <tr>
     <td rowspan="2"><p>RaBitQ</p></td>
     <td><p><code translate="no">rbq_query_bits</code></p></td>
     <td><p>Sets whether additional scalar quantization of a query vector is applied. If set to <code translate="no">0</code>, the query is used without quantization. If set to a value within [1, 8], the query is preprocessed using n-bit scalar quantization.</p></td>
     <td><p><strong>Type</strong>: Integer<br><strong>Range</strong>: [0, 8]<br><strong>Default value</strong>: <code translate="no">0</code></p></td>
     <td><p>The default <code translate="no">0</code> value provides maximum recall rate but slowest performance. We recommend testing values <code translate="no">0</code>, <code translate="no">8</code>, and <code translate="no">6</code>, as they provide similar recall rates with <code translate="no">6</code> being the fastest. Use smaller values for higher recall requirements.</p></td>
   </tr>
   <tr>
     <td><p><code translate="no">refine_k</code></p></td>
     <td><p>The refining process uses higher quality quantization to pick the needed number of nearest neighbors from a <code translate="no">refine_k</code> times larger pool of candidates chosen using IVF_RABITQ.</p></td>
     <td><p><strong>Type</strong>: Float<br><strong>Range</strong>: [1, <em>float_max</em>)<br><strong>Default value</strong>: <code translate="no">1</code></p></td>
     <td><p>Higher <code translate="no">refine_k</code> values decrease QPS but increase recall rate. Start with <code translate="no">1</code> and test values <code translate="no">2</code>, <code translate="no">3</code>, <code translate="no">4</code>, and <code translate="no">5</code> to find the optimal trade-off between QPS and recall for your dataset.</p></td>
   </tr>
</table>
