---
id: gaussian-decay.md
title: Gaußscher ZerfallCompatible with Milvus 2.6.x
summary: >-
  Gaußscher Zerfall, auch bekannt als normaler Zerfall, erzeugt die natürlichste
  Anpassung Ihrer Suchergebnisse. Ähnlich wie bei der menschlichen Sehkraft, die
  mit zunehmender Entfernung allmählich verschwimmt, erzeugt der Gaußsche
  Zerfall eine sanfte, glockenförmige Kurve, die die Relevanz sanft verringert,
  wenn sich die Elemente von Ihrem Idealpunkt entfernen. Dieser Ansatz ist
  ideal, wenn Sie einen ausgewogenen Abklingvorgang wünschen, bei dem Artikel,
  die knapp außerhalb Ihres bevorzugten Bereichs liegen, nicht hart bestraft
  werden, aber dennoch die Relevanz von weit entfernten Artikeln deutlich
  reduziert wird.
beta: Milvus 2.6.x
---
<h1 id="Gaussian-Decay" class="common-anchor-header">Gaußscher Zerfall<span class="beta-tag" style="background-color:rgb(0, 179, 255);color:white" translate="no">Compatible with Milvus 2.6.x</span><button data-href="#Gaussian-Decay" class="anchor-icon" translate="no">
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
    </button></h1><p>Gaußscher Zerfall, auch bekannt als normaler Zerfall, erzeugt die natürlichste Anpassung Ihrer Suchergebnisse. Ähnlich wie beim menschlichen Sehen, das mit zunehmender Entfernung allmählich verschwimmt, erzeugt der Gaußsche Zerfall eine sanfte, glockenförmige Kurve, die die Relevanz sanft verringert, wenn sich die Elemente von Ihrem Idealpunkt entfernen. Dieser Ansatz ist ideal, wenn Sie einen ausgewogenen Abklingvorgang wünschen, bei dem Artikel, die knapp außerhalb Ihres bevorzugten Bereichs liegen, nicht hart bestraft werden, aber dennoch die Relevanz weiter entfernter Artikel deutlich reduziert wird.</p>
<p>Im Gegensatz zu anderen Zerfallsrankern:</p>
<ul>
<li><p>Exponentieller Verfall fällt anfangs stark ab, was zu einer stärkeren anfänglichen Bestrafung führt.</p></li>
<li><p>Der lineare Verfall nimmt mit einer konstanten Rate ab, bis er den Wert Null erreicht, wodurch eine klare Grenze gesetzt wird.</p></li>
</ul>
<p>Gaußscher Zerfall bietet einen ausgewogenen, intuitiven Ansatz, der sich für die Nutzer natürlich anfühlt.</p>
<h2 id="When-to-use-Gaussian-decay" class="common-anchor-header">Wann wird Gaußscher Zerfall verwendet?<button data-href="#When-to-use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>Gaußscher Zerfall ist besonders effektiv für:</p>
<table>
   <tr>
     <th><p>Anwendungsfall</p></th>
     <th><p>Beispiel</p></th>
     <th><p>Warum Gaussian gut funktioniert</p></th>
   </tr>
   <tr>
     <td><p>Standortbezogene Suche</p></td>
     <td><p>Restaurant-Finder, Ladenlokalisierer</p></td>
     <td><p>Nachahmung der natürlichen menschlichen Wahrnehmung von Entfernungsrelevanz</p></td>
   </tr>
   <tr>
     <td><p>Empfehlungen zu Inhalten</p></td>
     <td><p>Artikelvorschläge basierend auf dem Veröffentlichungsdatum</p></td>
     <td><p>Allmähliche Abnahme der Relevanz mit zunehmendem Alter der Inhalte</p></td>
   </tr>
   <tr>
     <td><p>Produktauflistungen</p></td>
     <td><p>Artikel mit Preisen in der Nähe eines Ziels</p></td>
     <td><p>Sanfter Rückgang der Relevanz bei Preisabweichungen vom Ziel</p></td>
   </tr>
   <tr>
     <td><p>Abgleich von Fachwissen</p></td>
     <td><p>Auffinden von Fachleuten mit relevanter Erfahrung</p></td>
     <td><p>Ausgewogene Bewertung der Relevanz von Erfahrungen</p></td>
   </tr>
</table>
<p>Wenn Ihre Anwendung ein natürliches Gefühl von abnehmender Relevanz ohne harte Strafen oder strenge Grenzwerte erfordert, ist der Gaußsche Zerfall wahrscheinlich die beste Wahl.</p>
<h2 id="Bell-curve-principle" class="common-anchor-header">Prinzip der Glockenkurve<button data-href="#Bell-curve-principle" class="anchor-icon" translate="no">
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
    </button></h2><p>Der Gaußsche Zerfall erzeugt eine sanfte, glockenförmige Kurve, die die Relevanz mit zunehmender Entfernung von einem Idealpunkt allmählich verringert. Diese nach dem Mathematiker Carl Friedrich Gauß benannte Verteilung kommt in der Natur und in der Statistik häufig vor, was erklärt, warum sie sich für die menschliche Wahrnehmung so intuitiv anfühlt.</p>
<p>
  
   <span class="img-wrapper"> <img translate="no" src="/docs/v2.5.x/assets/gaussian-decay.png" alt="Gaussian Decay" class="doc-image" id="gaussian-decay" />
   </span> <span class="img-wrapper"> <span>Gaußscher Zerfall</span> </span></p>
<p>Das obige Diagramm zeigt, wie sich der Gauß'sche Zerfall auf das Ranking von Restaurants in einer mobilen Such-App auswirken würde:</p>
<ul>
<li><p><code translate="no">origin</code> (0 km): Ihr aktueller Standort, wo die Relevanz am höchsten ist (1,0).</p></li>
<li><p><code translate="no">offset</code> (±300 m): Die "perfekte Bewertungszone" um Sie herum - alle Restaurants in einem Umkreis von 300 Metern behalten ihre volle Relevanzbewertung (1,0), um sicherzustellen, dass nahe gelegene Optionen nicht unnötig für winzige Entfernungsunterschiede bestraft werden.</p></li>
<li><p><code translate="no">scale</code> (±2 km): Die Entfernung, bei der die Relevanz auf den Abklingwert sinkt - bei Restaurants, die genau 2 Kilometer entfernt sind, wird die Relevanzbewertung halbiert (0,5).</p></li>
<li><p><code translate="no">decay</code> (0.5): Die Punktzahl bei der Skalendistanz - dieser Parameter steuert im Wesentlichen, wie schnell die Punktzahlen mit der Entfernung abnehmen.</p></li>
</ul>
<p>Wie Sie der Kurve entnehmen können, nimmt die Relevanz von Restaurants in mehr als 2 km Entfernung weiter ab, erreicht aber nie ganz den Wert Null. Selbst Restaurants in einer Entfernung von 4 bis 5 Kilometern behalten eine gewisse minimale Relevanz, so dass ausgezeichnete, aber weit entfernte Restaurants immer noch in Ihren Ergebnissen erscheinen (wenn auch in einer niedrigeren Rangfolge).</p>
<p>Dieses Verhalten ahmt nach, wie Menschen natürlicherweise über die Relevanz von Entfernungen denken - nahe gelegene Orte werden bevorzugt, aber wir sind bereit, für außergewöhnliche Optionen weiter zu reisen.</p>
<h2 id="Formula" class="common-anchor-header">Formel<button data-href="#Formula" class="anchor-icon" translate="no">
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
    </button></h2><p>Die mathematische Formel für die Berechnung einer Gauß'schen Zerfallszahl lautet:</p>
<p>$$ S(doc) = \exp\left( -\frac{\left( \max\left(0, \left|fieldvalue_{doc} - origin\right| - offset \right) \right)^2}{2\sigma^2} \right) $$</p>
<p>Wobei:</p>
<p>$$ \sigma^2 = -\frac{scale^2}{2 \cdot \ln(decay)} $$</p>
<p>In einfacher Sprache ausgedrückt:</p>
<ol>
<li><p>Berechne, wie weit der Feldwert vom Ursprung entfernt ist: $|Feldwert_{doc} - Ursprung|$</p></li>
<li><p>Subtrahiere den Versatz (falls vorhanden), aber gehe nie unter Null: $\max(0, Abstand - Versatz)$</p></li>
<li><p>Quadriere diese angepasste Distanz: $(angepasste_Distanz)^2$</p></li>
<li><p>Dividiere durch $2\sigma^2$, das aus deinen Skalen- und Abklingparametern berechnet wird</p></li>
<li><p>Nehmen Sie den negativen Exponenten, der einen Wert zwischen 0 und 1 ergibt: $\exp(-wert)$</p></li>
</ol>
<p>Die Berechnung von $\sigma^2$ wandelt Ihre Skalen- und Zerfallsparameter in die quadrierte Standardabweichung der Gaußschen Verteilung um. Dadurch erhält die Funktion ihre charakteristische Glockenform.</p>
<h2 id="Use-Gaussian-decay" class="common-anchor-header">Verwendung des Gaußschen Abklingens<button data-href="#Use-Gaussian-decay" class="anchor-icon" translate="no">
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
    </button></h2><p>Gaußscher Zerfall kann sowohl auf die Standard-Vektorsuche als auch auf hybride Suchoperationen in Milvus angewendet werden. Im Folgenden finden Sie die wichtigsten Codeschnipsel für die Implementierung dieser Funktion.</p>
<div class="alert note">
<p>Bevor Sie die Abklingfunktionen verwenden, müssen Sie zunächst eine Sammlung mit geeigneten numerischen Feldern (wie Zeitstempel, Entfernungen usw.) erstellen, die für die Abklingberechnungen verwendet werden sollen. Vollständige Arbeitsbeispiele, einschließlich der Einrichtung der Sammlung, der Schemadefinition und der Dateneinfügung, finden Sie im <a href="/docs/de/tutorial-implement-a-time-based-ranking-in-milvus.md">Tutorial: Zeitbasiertes Ranking in Milvus implementieren</a>.</p>
</div>
<h3 id="Create-a-decay-ranker" class="common-anchor-header">Erstellen Sie einen Decay Ranker</h3><p>Nachdem Sie Ihre Sammlung mit einem numerischen Feld eingerichtet haben (in diesem Beispiel <code translate="no">distance</code> in Metern vom Benutzer), erstellen Sie einen Gauß'schen Zerfallsranker:</p>
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
<h3 id="Apply-to-standard-vector-search" class="common-anchor-header">Auf die Standard-Vektorsuche anwenden</h3><p>Nachdem Sie Ihren Decay Ranker definiert haben, können Sie ihn bei Suchvorgängen anwenden, indem Sie ihn an den Parameter <code translate="no">ranker</code> übergeben:</p>
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
<h3 id="Apply-to-hybrid-search" class="common-anchor-header">Auf hybride Suche anwenden</h3><p>Decay Rankers können auch auf hybride Suchoperationen angewendet werden, die mehrere Vektorfelder kombinieren:</p>
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
<p>Weitere Informationen zu hybriden Suchoperationen finden Sie unter <a href="/docs/de/multi-vector-search.md">Hybride Suche mit mehreren Vektoren</a>.</p>
