---
id: gaussian-decay.md
title: Décroissance gaussienneCompatible with Milvus 2.6.x
summary: >-
  La décroissance gaussienne, également connue sous le nom de décroissance
  normale, crée l'ajustement le plus naturel de vos résultats de recherche. À
  l'instar de la vision humaine qui s'estompe progressivement avec la distance,
  la décroissance gaussienne crée une courbe lisse, en forme de cloche, qui
  réduit doucement la pertinence à mesure que les éléments s'éloignent de votre
  point idéal. Cette approche est idéale lorsque vous souhaitez une décroissance
  équilibrée qui ne pénalise pas durement les éléments situés juste en dehors de
  votre plage préférée, mais qui réduit tout de même de manière significative la
  pertinence des éléments éloignés.
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">Décroissance gaussienne<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>La décroissance gaussienne, également connue sous le nom de décroissance normale, crée l'ajustement le plus naturel de vos résultats de recherche. À l'instar de la vision humaine qui s'estompe progressivement avec la distance, la décroissance gaussienne crée une courbe lisse en forme de cloche qui réduit doucement la pertinence au fur et à mesure que les éléments s'éloignent de votre point idéal. Cette approche est idéale lorsque vous souhaitez une décroissance équilibrée qui ne pénalise pas durement les éléments situés juste en dehors de votre plage préférée, mais qui réduit tout de même de manière significative la pertinence des éléments éloignés.</p>
<p>Contrairement à d'autres outils de classement de la décroissance :</p>
<ul>
<li><p>La décroissance exponentielle diminue fortement au début, ce qui crée une pénalité initiale plus forte.</p></li>
<li><p>La décroissance linéaire diminue à un rythme constant jusqu'à atteindre zéro, ce qui crée une limite claire.</p></li>
</ul>
<p>La décroissance gaussienne offre une approche plus équilibrée et intuitive qui semble naturelle aux utilisateurs.</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">Quand utiliser la décroissance gaussienne ?<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>La décroissance gaussienne est particulièrement efficace dans les cas suivants :</p>
<table>
   <tr>
     <th><p>Cas d'utilisation</p></th>
     <th><p>Exemple de cas d'utilisation</p></th>
     <th><p>Pourquoi la décroissance gaussienne fonctionne bien</p></th>
   </tr>
   <tr>
     <td><p>Recherches basées sur la localisation</p></td>
     <td><p>Recherche de restaurants, de magasins</p></td>
     <td><p>Imite la perception humaine naturelle de la pertinence de la distance</p></td>
   </tr>
   <tr>
     <td><p>Recommandations de contenu</p></td>
     <td><p>Suggestions d'articles basées sur la date de publication</p></td>
     <td><p>Diminution progressive de la pertinence au fur et à mesure que le contenu vieillit</p></td>
   </tr>
   <tr>
     <td><p>Listes de produits</p></td>
     <td><p>Articles dont le prix est proche d'une cible</p></td>
     <td><p>Diminution progressive de la pertinence lorsque les prix s'écartent de la cible</p></td>
   </tr>
   <tr>
     <td><p>Correspondance d'expertise</p></td>
     <td><p>Recherche de professionnels possédant une expérience pertinente</p></td>
     <td><p>Évaluation équilibrée de la pertinence de l'expérience</p></td>
   </tr>
</table>
<p>Si votre application nécessite un sentiment naturel de déclin de la pertinence sans pénalités sévères ou seuils stricts, la décroissance gaussienne est probablement votre meilleur choix.</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">Principe de la courbe en cloche<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>La décroissance gaussienne crée une courbe lisse, en forme de cloche, qui réduit progressivement la pertinence à mesure que la distance augmente par rapport à un point idéal. Nommée d'après le mathématicien Carl Friedrich Gauss, cette distribution apparaît fréquemment dans la nature et les statistiques, ce qui explique pourquoi elle est si intuitive pour la perception humaine.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>Décroissance gaussienne</span> </span></p>
<p>Le graphique ci-dessus montre comment la décroissance gaussienne affecterait le classement des restaurants dans une application de recherche mobile :</p>
<ul>
<li><p><code translate="no">origin</code> (0 km) : Votre emplacement actuel, où la pertinence est maximale (1,0).</p></li>
<li><p><code translate="no">offset</code> (±300 m) : La "zone de score parfait" autour de vous - tous les restaurants situés dans un rayon de 300 mètres conservent des scores de pertinence complets (1,0), ce qui garantit que les options très proches ne sont pas inutilement pénalisées par de minuscules différences de distance.</p></li>
<li><p><code translate="no">scale</code> (±2 km) : La distance à laquelle la pertinence chute à la valeur de décroissance - les restaurants situés à exactement 2 kilomètres voient leur score de pertinence divisé par deux (0,5).</p></li>
<li><p><code translate="no">decay</code> (0.5) : Le score à la distance d'échelle - ce paramètre contrôle essentiellement la vitesse à laquelle les scores diminuent avec la distance.</p></li>
</ul>
<p>Comme vous pouvez le voir sur la courbe, la pertinence des restaurants situés à plus de 2 km continue de diminuer sans jamais atteindre zéro. Même les restaurants situés à 4 ou 5 kilomètres conservent une pertinence minimale, ce qui permet à d'excellents restaurants éloignés d'apparaître dans les résultats (bien que moins bien classés).</p>
<p>Ce comportement imite la façon dont les gens pensent naturellement à la pertinence de la distance - les endroits proches sont préférés, mais nous sommes prêts à voyager plus loin pour des options exceptionnelles.</p>
<h2 id="Formula" class="common-anchor-header">Formule<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>La formule mathématique permettant de calculer un score de décroissance gaussienne est la suivante :</p>
<p>$$ S(doc) = \exp\left( -\frac{\left( \max\left(0, \left|fieldvalue_{doc} - originright| - offset \right) \right)^2}{2\sigma^2} \Ndroite) $$</p>
<p>Où :</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(decay)} $$</p>
<p>En clair, il s'agit de calculer la distance qui sépare la valeur du champ de celle de la valeur du champ :</p>
<ol>
<li><p>Calculer la distance entre la valeur du champ et l'origine : $|valeur_du_champ_{doc} - origine|$</p></li>
<li><p>Soustraire le décalage (le cas échéant) sans jamais descendre en dessous de zéro : $\max(0, distance - décalage)$.</p></li>
<li><p>Élever au carré la distance ajustée : $(adjusted_distance)^2</p></li>
<li><p>Diviser par $2\sigma^2$, qui est calculé à partir de vos paramètres d'échelle et de décroissance.</p></li>
<li><p>Prendre l'exposant négatif, qui donne une valeur comprise entre 0 et 1 : $\exp(-valeur)$.</p></li>
</ol>
<p>Le calcul de $\sigma^2$ convertit vos paramètres d'échelle et de décroissance en écart-type au carré pour la distribution gaussienne. C'est ce qui donne à la fonction sa forme caractéristique de cloche.</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">Utiliser la décroissance gaussienne<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>La décroissance gaussienne peut être appliquée aux opérations de recherche vectorielle standard et de recherche hybride dans Milvus. Vous trouverez ci-dessous les principaux extraits de code permettant de mettre en œuvre cette fonctionnalité.</p>
<div class="alert note">
<p>Avant d'utiliser les fonctions de décroissance, vous devez d'abord créer une collection avec les champs numériques appropriés (comme les horodatages, les distances, etc.) qui seront utilisés pour les calculs de décroissance. Pour des exemples de travail complets comprenant la configuration de la collection, la définition du schéma et l'insertion de données, reportez-vous au <a href="/docs/fr/tutorial-implement-a-time-based-ranking-in-milvus.md">didacticiel : Mise en œuvre du classement basé sur le temps dans Milvus</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Créer un classeur de décroissance</h3><p>Une fois votre collection configurée avec un champ numérique (dans cet exemple, <code translate="no">distance</code> en mètres de l'utilisateur), créez un classificateur de décroissance gaussienne :</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Appliquer à la recherche vectorielle standard</h3><p>Après avoir défini votre classificateur de décroissance, vous pouvez l'appliquer lors des opérations de recherche en le passant au paramètre <code translate="no">ranker</code>:</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Appliquer à la recherche hybride</h3><p>Les classificateurs de décroissance peuvent également être appliqués aux opérations de recherche hybride qui combinent plusieurs champs de vecteurs :</p>
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
<p>Pour plus d'informations sur les opérations de recherche hybride, reportez-vous à la section <a href="/docs/fr/multi-vector-search.md">Recherche hybride multivectorielle</a>.</p>
