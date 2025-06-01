---
id: linear-decay.md
title: Décroissance linéaireCompatible with Milvus 2.6.x
summary: >-
  La décroissance linéaire crée un déclin en ligne droite qui se termine à un
  point zéro absolu dans vos résultats de recherche. À l'instar d'un compte à
  rebours d'un événement à venir dont la pertinence s'estompe progressivement
  jusqu'à ce que l'événement soit passé, la décroissance linéaire applique une
  réduction prévisible et régulière de la pertinence au fur et à mesure que les
  éléments s'éloignent de votre point idéal, jusqu'à ce qu'ils disparaissent
  complètement. Cette approche est idéale lorsque vous souhaitez obtenir un taux
  de décroissance cohérent avec une limite claire, garantissant que les éléments
  dépassant un certain seuil sont complètement exclus des résultats.
beta: Milvus 2.6.x
---
<h1 id="Linear-Decay" class="common-anchor-header">Décroissance linéaire<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Linear-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>La décroissance linéaire crée un déclin en ligne droite qui se termine à un point zéro absolu dans vos résultats de recherche. À l'instar d'un compte à rebours d'un événement à venir dont la pertinence s'estompe progressivement jusqu'à ce que l'événement soit passé, la décroissance linéaire applique une réduction prévisible et régulière de la pertinence au fur et à mesure que les éléments s'éloignent de votre point idéal, jusqu'à ce qu'ils disparaissent complètement. Cette approche est idéale lorsque vous souhaitez un taux de décroissance cohérent avec une limite claire, garantissant que les éléments dépassant une certaine limite sont complètement exclus des résultats.</p>
<p>Contrairement à d'autres fonctions de désintégration :</p>
<ul>
<li><p>La désintégration gaussienne suit une courbe en cloche qui se rapproche progressivement de zéro sans jamais l'atteindre</p></li>
<li><p>La décroissance exponentielle maintient une longue queue de pertinence minimale qui s'étend indéfiniment.</p></li>
</ul>
<p>La décroissance linéaire crée un point final unique, ce qui la rend particulièrement efficace pour les applications comportant des limites naturelles ou des échéances.</p>
<h2 id="When-to-use-linear-decay" class="common-anchor-header">Quand utiliser la décroissance linéaire ?<button data-href="#When-to-use-linear-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>La décroissance linéaire est particulièrement efficace pour :</p>
<table>
   <tr>
     <th><p>Cas d'utilisation</p></th>
     <th><p>Exemple de cas d'utilisation</p></th>
     <th><p>Pourquoi la décroissance linéaire fonctionne bien</p></th>
   </tr>
   <tr>
     <td><p>Listes d'événements</p></td>
     <td><p>Plateformes de vente de billets de concert</p></td>
     <td><p>Crée une limite claire pour les événements trop éloignés dans le temps</p></td>
   </tr>
   <tr>
     <td><p>Offres à durée limitée</p></td>
     <td><p>Ventes flash, promotions</p></td>
     <td><p>Permet de s'assurer que les offres expirées ou sur le point d'expirer n'apparaissent pas.</p></td>
   </tr>
   <tr>
     <td><p>Rayon de livraison</p></td>
     <td><p>Livraison de nourriture, services de messagerie</p></td>
     <td><p>Permet d'imposer des limites géographiques strictes</p></td>
   </tr>
   <tr>
     <td><p>Contenus limités par l'âge</p></td>
     <td><p>Plateformes de rencontres, services de médias</p></td>
     <td><p>Établit des seuils d'âge fermes</p></td>
   </tr>
</table>
<p>Choisissez la décroissance linéaire lorsque :</p>
<ul>
<li><p>Votre application a une limite naturelle, une date limite ou un seuil.</p></li>
<li><p>Les éléments dépassant un certain seuil doivent être complètement exclus des résultats.</p></li>
<li><p>Vous avez besoin d'un taux prévisible et cohérent de déclin de la pertinence.</p></li>
<li><p>Les utilisateurs doivent voir une démarcation claire entre les éléments pertinents et ceux qui ne le sont pas.</p></li>
</ul>
<h2 id="Steady-decline-principle" class="common-anchor-header">Principe de décroissance régulière<button data-href="#Steady-decline-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>La décroissance linéaire crée une baisse en ligne droite qui diminue à un taux constant jusqu'à atteindre exactement zéro. Ce modèle apparaît dans de nombreux scénarios quotidiens tels que les comptes à rebours, l'épuisement des stocks et l'approche d'échéances où la pertinence a un point d'expiration clair.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/linear-decay.png" alt="Linear Decay" class="doc-image" id="linear-decay" />
   </span> <span class="img-wrapper"> <span>Décroissance linéaire</span> </span></p>
<p>Le graphique ci-dessus montre comment la décroissance linéaire affecte les listes d'événements sur une plateforme de billetterie :</p>
<ul>
<li><p><code translate="no">origin</code> (date actuelle) : Le moment présent, où la pertinence est à son maximum (1.0).</p></li>
<li><p><code translate="no">offset</code> (1 jour) : La "fenêtre des événements immédiats" - tous les événements se déroulant le jour suivant conservent leur score de pertinence maximal (1,0), ce qui garantit que les événements très imminents ne sont pas pénalisés par de légers décalages temporels.</p></li>
<li><p><code translate="no">decay</code> (0.5) : Le score à la distance de l'échelle - ce paramètre contrôle le taux de déclin de la pertinence.</p></li>
<li><p><code translate="no">scale</code> (10 jours) : Le délai à partir duquel la pertinence tombe à la valeur de décroissance - les événements situés à 10 jours de distance voient leur score de pertinence divisé par deux (0,5).</p></li>
</ul>
<p>Comme le montre la courbe linéaire, les événements qui se produisent dans plus de 16 jours ont une pertinence nulle et n'apparaissent pas du tout dans les résultats de recherche. Cela crée une limite claire qui garantit que les utilisateurs ne voient que les événements pertinents à venir dans une fenêtre temporelle définie.</p>
<p>Ce comportement reflète le fonctionnement habituel de la planification d'événements : les événements imminents sont les plus pertinents, les événements des semaines à venir ont une importance décroissante et les événements trop éloignés dans le temps (ou déjà passés) ne devraient pas apparaître du tout.</p>
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
    </button></h2><p>La formule mathématique permettant de calculer un score de décroissance linéaire est la suivante :</p>
<p>$$ S(doc) = \max\gauche( \frac{s - \max(0, |fieldvalue_{doc} - origin| - offset)}{s}, 0 \ndroite) $$</p>
<p>Où :</p>
<p>$$ s = \frac {scale}{(1.0 - decay)} $$</p>
<p>En clair, il s'agit de calculer la distance qui sépare la valeur du champ de celle de la valeur du champ :</p>
<ol>
<li><p>Calculer la distance entre la valeur du champ et l'origine : $|fieldvalue_{doc} - origin|$.</p></li>
<li><p>Soustraire le décalage (le cas échéant) sans jamais descendre en dessous de zéro : $\max(0, distance - décalage)$.</p></li>
<li><p>Déterminer le paramètre $s$ à partir des valeurs d'échelle et de décroissance.</p></li>
<li><p>Soustrayez la distance ajustée de $s$ et divisez par $s$.</p></li>
<li><p>Veillez à ce que le résultat ne soit jamais inférieur à zéro : $\max(result, 0)$.</p></li>
</ol>
<p>Le calcul de $s$ transforme vos paramètres d'échelle et de décroissance en un point où le score atteint zéro. Par exemple, avec une décroissance de 0,5 et une échelle de 7, le score atteindra exactement zéro à une distance de 14 (deux fois la valeur de l'échelle).</p>
<h2 id="Use-linear-decay" class="common-anchor-header">Utiliser la décroissance linéaire<button data-href="#Use-linear-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>La décroissance linéaire peut être appliquée aux opérations de recherche vectorielle standard et de recherche hybride dans Milvus. Vous trouverez ci-dessous les principaux extraits de code permettant de mettre en œuvre cette fonctionnalité.</p>
<div class="alert note">
<p>Avant d'utiliser les fonctions de décroissance, vous devez d'abord créer une collection avec les champs numériques appropriés (comme les horodatages, les distances, etc.) qui seront utilisés pour les calculs de décroissance. Pour des exemples de travail complets comprenant la configuration de la collection, la définition du schéma et l'insertion de données, reportez-vous au <a href="/docs/fr/tutorial-implement-a-time-based-ranking-in-milvus.md">didacticiel sur</a> le <a href="/docs/fr/tutorial-implement-a-time-based-ranking-in-milvus.md">classificateur de décroissance</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Créer un classificateur de décroissance</h3><p>Une fois votre collection configurée avec un champ numérique (dans cet exemple, <code translate="no">event_date</code> comme secondes à partir de maintenant), créez un classificateur de décroissance linéaire :</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> Function, FunctionType
<span class="hljs-keyword">import</span> time

<span class="hljs-comment"># Calculate current time</span>
current_time = <span class="hljs-built_in">int</span>(time.time())

<span class="hljs-comment"># Create a linear decay ranker for event listings</span>
ranker = Function(
    name=<span class="hljs-string">&quot;event_relevance&quot;</span>,               <span class="hljs-comment"># Function identifier</span>
    input_field_names=[<span class="hljs-string">&quot;event_date&quot;</span>],     <span class="hljs-comment"># Numeric field to use</span>
    function_type=FunctionType.RERANK,    <span class="hljs-comment"># Function type. Must be RERANK</span>
    params={
        <span class="hljs-string">&quot;reranker&quot;</span>: <span class="hljs-string">&quot;decay&quot;</span>,              <span class="hljs-comment"># Specify decay reranker</span>
        <span class="hljs-string">&quot;function&quot;</span>: <span class="hljs-string">&quot;linear&quot;</span>,             <span class="hljs-comment"># Choose linear decay</span>
        <span class="hljs-string">&quot;origin&quot;</span>: current_time,           <span class="hljs-comment"># Current time</span>
        <span class="hljs-string">&quot;offset&quot;</span>: <span class="hljs-number">12</span> * <span class="hljs-number">60</span> * <span class="hljs-number">60</span>,           <span class="hljs-comment"># 12 hour immediate events window</span>
        <span class="hljs-string">&quot;decay&quot;</span>: <span class="hljs-number">0.5</span>,                     <span class="hljs-comment"># Half score at scale distance</span>
        <span class="hljs-string">&quot;scale&quot;</span>: <span class="hljs-number">7</span> * <span class="hljs-number">24</span> * <span class="hljs-number">60</span> * <span class="hljs-number">60</span>         <span class="hljs-comment"># 7 days (in seconds)</span>
    }
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Appliquer à la recherche vectorielle standard</h3><p>Après avoir défini votre classificateur de décroissance, vous pouvez l'appliquer lors des opérations de recherche en le passant au paramètre <code translate="no">ranker</code>:</p>
<pre><code translate="no" class="language-python"><span class="hljs-comment"># Apply decay ranker to vector search</span>
result = milvus_client.search(
    collection_name,
    data=[<span class="hljs-string">&quot;music concerts&quot;</span>],              <span class="hljs-comment"># Query text</span>
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,                   <span class="hljs-comment"># Vector field to search</span>
    limit=<span class="hljs-number">10</span>,                             <span class="hljs-comment"># Number of results</span>
    output_fields=[<span class="hljs-string">&quot;title&quot;</span>, <span class="hljs-string">&quot;venue&quot;</span>, <span class="hljs-string">&quot;event_date&quot;</span>], <span class="hljs-comment"># Fields to return</span>
    ranker=ranker,                        <span class="hljs-comment"># Apply the decay ranker</span>
    consistency_level=<span class="hljs-string">&quot;Strong&quot;</span>
)
<button class="copy-code-btn"></button></code></pre>
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Appliquer à la recherche hybride</h3><p>Les classificateurs de décroissance peuvent également être appliqués aux opérations de recherche hybride qui combinent plusieurs champs de vecteurs :</p>
<pre><code translate="no" class="language-python"><span class="hljs-keyword">from</span> pymilvus <span class="hljs-keyword">import</span> AnnSearchRequest

<span class="hljs-comment"># Define dense vector search request</span>
dense = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;music concerts&quot;</span>],
    anns_field=<span class="hljs-string">&quot;dense&quot;</span>,
    param={},
    limit=<span class="hljs-number">10</span>
)

<span class="hljs-comment"># Define sparse vector search request</span>
sparse = AnnSearchRequest(
    data=[<span class="hljs-string">&quot;music concerts&quot;</span>],
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
    output_fields=[<span class="hljs-string">&quot;title&quot;</span>, <span class="hljs-string">&quot;venue&quot;</span>, <span class="hljs-string">&quot;event_date&quot;</span>]
)
<button class="copy-code-btn"></button></code></pre>
<p>Pour plus d'informations sur les opérations de recherche hybride, reportez-vous à la section <a href="/docs/fr/multi-vector-search.md">Recherche hybride multivectorielle</a>.</p>
