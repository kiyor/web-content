---
id: rrf-ranker.md
title: RRF RankerCompatible with Milvus 2.6.x
summary: >-
  Reciprocal Rank Fusion (RRF) Ranker est une stratégie de reclassement pour la
  recherche hybride Milvus qui équilibre les résultats de plusieurs chemins de
  recherche vectorielle en fonction de leurs positions de classement plutôt que
  de leurs scores de similarité bruts. À l'instar d'un tournoi sportif qui prend
  en compte les classements des joueurs plutôt que les statistiques
  individuelles, RRF Ranker combine les résultats de recherche en fonction du
  classement de chaque élément dans les différents chemins de recherche, créant
  ainsi un classement final juste et équilibré.
beta: Milvus 2.6.x
---
<h1 id="RRF-Ranker" class="common-anchor-header">RRF Ranker<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h1><p>Reciprocal Rank Fusion (RRF) Ranker est une stratégie de reclassement pour la recherche hybride Milvus qui équilibre les résultats de plusieurs chemins de recherche vectorielle en fonction de leurs positions de classement plutôt que de leurs scores de similarité bruts. À l'instar d'un tournoi sportif qui prend en compte les classements des joueurs plutôt que les statistiques individuelles, RRF Ranker combine les résultats de recherche en fonction du classement de chaque élément dans les différents chemins de recherche, créant ainsi un classement final juste et équilibré.</p>
<h2 id="When-to-use-RRF-Ranker" class="common-anchor-header">Quand utiliser RRF Ranker ?<button data-href="#When-to-use-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>RRF Ranker est spécialement conçu pour les scénarios de recherche hybride dans lesquels vous souhaitez équilibrer les résultats de plusieurs chemins de recherche vectoriels sans attribuer de poids d'importance explicites. Il est particulièrement efficace pour :</p>
<table>
   <tr>
     <th><p>Cas d'utilisation</p></th>
     <th><p>Exemple de cas d'utilisation</p></th>
     <th><p>Pourquoi RRF Ranker fonctionne bien</p></th>
   </tr>
   <tr>
     <td><p>Recherche multimodale avec la même importance</p></td>
     <td><p>Recherche image-texte où les deux modalités ont la même importance</p></td>
     <td><p>Équilibre les résultats sans nécessiter d'affectations de poids arbitraires</p></td>
   </tr>
   <tr>
     <td><p>Recherche vectorielle d'ensemble</p></td>
     <td><p>Combinaison des résultats de différents modèles d'intégration</p></td>
     <td><p>Fusion démocratique des classements sans favoriser la distribution des scores d'un modèle particulier</p></td>
   </tr>
   <tr>
     <td><p>Recherche multilingue</p></td>
     <td><p>Recherche de documents dans plusieurs langues</p></td>
     <td><p>Classement équitable des résultats indépendamment des caractéristiques d'intégration propres à chaque langue</p></td>
   </tr>
   <tr>
     <td><p>Recommandations d'experts</p></td>
     <td><p>Combinaison de recommandations provenant de plusieurs systèmes experts</p></td>
     <td><p>Crée des classements consensuels lorsque différents systèmes utilisent des méthodes de notation incomparables.</p></td>
   </tr>
</table>
<p>Si votre application de recherche hybride nécessite d'équilibrer démocratiquement plusieurs chemins de recherche sans attribuer de poids explicites, RRF Ranker est votre choix idéal.</p>
<h2 id="Mechanism-of-RRF-Ranker" class="common-anchor-header">Mécanisme de RRF Ranker<button data-href="#Mechanism-of-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>Le flux de travail principal de la stratégie RRFRanker est le suivant :</p>
<ol>
<li><p><strong>Collecte des classements de recherche</strong>: Collecte des classements des résultats de chaque chemin de recherche vectorielle (rang_1, rang_2).</p></li>
<li><p><strong>Fusionner les classements</strong>: Convertir les classements de chaque chemin (rang_rrf_1, rang_rrf_2) selon une formule .</p>
<p>La formule de calcul fait intervenir <em>N</em>, qui représente le nombre d'extractions. <em>ranki</em><em>(d)</em> est la position de classement du document <em>d</em> généré par le <em>i(ème</em> ) extracteur. <em>k</em> est un paramètre de lissage généralement fixé à 60.</p></li>
<li><p><strong>Classement agrégé</strong>: Reclasser les résultats de la recherche sur la base des classements combinés pour produire les résultats finaux.</p></li>
</ol>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/rrf-ranker.png" alt="Rrf Ranker" class="doc-image" id="rrf-ranker" />
   </span> <span class="img-wrapper"> <span>Classeur RRF</span> </span></p>
<h2 id="Example-of-RRF-Ranker" class="common-anchor-header">Exemple de classement RRF<button data-href="#Example-of-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>Cet exemple illustre une recherche hybride (topK=5) sur des vecteurs peu denses et montre comment la stratégie RRFRanker reclasse les résultats de deux recherches ANN.</p>
<ul>
<li>Résultats de la recherche ANN sur des vecteurs de textes peu denses （topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Rang (clair)</strong></p></th>
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
<li>Résultats de la recherche ANN sur des vecteurs denses de textes （topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Rang (dense)</strong></p></th>
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
<li>Utilisez la méthode RRF pour réorganiser les classements des deux ensembles de résultats de recherche. Supposez que le paramètre de lissage <code translate="no">k</code> est fixé à 60.</li>
</ul>
<table>
   <tr>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Score (clairsemé)</strong></p></th>
     <th><p><strong>Score (dense)</strong></p></th>
     <th><p><strong>Score final</strong></p></th>
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
     <td><p>N/A</p></td>
     <td><p>1/(60+2) = 0.01613</p></td>
   </tr>
   <tr>
     <td><p>150</p></td>
     <td><p>3</p></td>
     <td><p>N/A</p></td>
     <td><p>1/(60+3) = 0.01587</p></td>
   </tr>
   <tr>
     <td><p>110</p></td>
     <td><p>N/A</p></td>
     <td><p>3</p></td>
     <td><p>1/(60+3) = 0.01587</p></td>
   </tr>
   <tr>
     <td><p>250</p></td>
     <td><p>N/A</p></td>
     <td><p>5</p></td>
     <td><p>1/(60+5) = 0.01554</p></td>
   </tr>
</table>
<ul>
<li>Les résultats finaux après reranking（topK=5)：</li>
</ul>
<table>
   <tr>
     <th><p><strong>Rang</strong></p></th>
     <th><p><strong>ID</strong></p></th>
     <th><p><strong>Score final</strong></p></th>
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
<h2 id="Usage-of-RRF-Ranker" class="common-anchor-header">Utilisation du classificateur RRF<button data-href="#Usage-of-RRF-Ranker" class="anchor-icon" translate="no">
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
    </button></h2><p>Lorsque vous utilisez la stratégie de reclassement RRF, vous devez configurer le paramètre <code translate="no">k</code>. Il s'agit d'un paramètre de lissage qui peut modifier efficacement les poids relatifs de la recherche en texte intégral par rapport à la recherche vectorielle. La valeur par défaut de ce paramètre est 60, et il peut être ajusté dans une plage de (0, 16384). La valeur doit être un nombre à virgule flottante. La valeur recommandée est comprise entre [10 et 100]. Bien que <code translate="no">k=60</code> soit un choix courant, la valeur optimale de <code translate="no">k</code> peut varier en fonction de vos applications et ensembles de données spécifiques. Nous vous recommandons de tester et d'ajuster ce paramètre en fonction de votre cas d'utilisation spécifique afin d'obtenir les meilleures performances.</p>
<h3 id="Create-an-RRF-Ranker" class="common-anchor-header">Créer un classificateur RRF</h3><p>Une fois votre collection configurée avec plusieurs champs vectoriels, créez un Ranker RRF avec un paramètre de lissage approprié :</p>
<div class="multipleCode">
   <a href="#python">Python</a> <a href="#java">Java</a> <a href="#go">Go</a> <a href="#javascript">NodeJS</a> <a href="#bash">cURL</a></div>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Appliquer à la recherche hybride</h3><p>RRF Ranker est conçu spécifiquement pour les opérations de recherche hybride qui combinent plusieurs champs vectoriels. Voici comment l'utiliser dans une recherche hybride :</p>
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
<p>Pour plus d'informations sur la recherche hybride, reportez-vous à la section <a href="/docs/fr/multi-vector-search.md">Recherche hybride multi-vecteurs</a>.</p>
