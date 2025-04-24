---
id: multi_tenancy.md
related_key: multi-tenancy
summary: Multi-tenancy in Milvus.
title: Strategie multi-tenancy
---
<h1 id="Multi-tenancy-strategies" class="common-anchor-header">Strategie multi-tenancy<button data-href="#Multi-tenancy-strategies" class="anchor-icon" translate="no">
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
    </button></h1><p>In molti casi d'uso, gli sviluppatori vogliono gestire un cluster Milvus e servire più tenancy, come un paio di team di prodotto o milioni di utenti finali. Questa guida illustra alcune strategie diverse per ottenere la multi-tenancy su Milvus.</p>
<p>Milvus è progettato per supportare la multi-tenancy a livello di database, collezione o partizione. L'obiettivo della multi-tenancy è quello di separare i dati e le risorse tra loro. L'implementazione della multi-tenancy a diversi livelli può raggiungere un diverso grado di isolamento, ma comporta anche un diverso overhead. Qui spieghiamo i loro compromessi.</p>
<h2 id="Database-oriented-multi-tenancy" class="common-anchor-header">Multi-tenancy orientata al database<button data-href="#Database-oriented-multi-tenancy" class="anchor-icon" translate="no">
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
    </button></h2><p>Dalla versione 2.2.9 di Milvus, è possibile creare più database in un singolo cluster Milvus. Questa funzione consente di ottenere una multi-tenancy orientata al database, assegnando un database per ogni tenant, in modo che questi possano creare le proprie collezioni. Questo approccio offre il miglior isolamento dei dati e delle risorse per i tenant, ma è limitato a 64 database in un cluster al massimo.</p>
<h2 id="Collection-oriented-multi-tenancy" class="common-anchor-header">Multi-tenancy orientata alle collezioni<button data-href="#Collection-oriented-multi-tenancy" class="anchor-icon" translate="no">
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
    </button></h2><p>Esistono due modi possibili per ottenere la multi-tenancy orientata alle collezioni.</p>
<h3 id="One-collection-for-all-tenants" class="common-anchor-header">Una collezione per tutti i tenant</h3><p>L'uso di una singola collezione per implementare la multi-tenancy, aggiungendo un campo tenant per distinguere i tenant, è un'opzione semplice. Quando si effettua una ricerca RNA per uno specifico tenant, si aggiunge un'espressione di filtro per filtrare tutte le entità che appartengono ad altri tenant. Questo è il modo più semplice per ottenere la multi-tenancy. Tuttavia, occorre tenere presente che le prestazioni del filtro possono diventare il collo di bottiglia delle ricerche ANN. Per migliorare le prestazioni della ricerca, si può ottimizzare con la multi-tenancy orientata alle partizioni.</p>
<h3 id="One-collection-per-tenant" class="common-anchor-header">Una raccolta per ogni tenancy</h3><p>Un altro approccio consiste nel creare una collezione per ogni tenant per memorizzare i propri dati, invece di memorizzare i dati di tutti i tenant in una singola collezione. In questo modo si ottiene un migliore isolamento dei dati e migliori prestazioni di interrogazione. Tuttavia, bisogna tenere presente che questo approccio richiede più risorse per la pianificazione ed è limitato a un massimo di 10.000 raccolte in un cluster.</p>
<h2 id="Partition-oriented-multi-tenancy" class="common-anchor-header">Multi-tenancy orientata alle partizioni<button data-href="#Partition-oriented-multi-tenancy" class="anchor-icon" translate="no">
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
    </button></h2><p>Esistono due modi per ottenere la multi-tenancy orientata alle partizioni:</p>
<h3 id="One-partition-per-tenant" class="common-anchor-header">Una partizione per tenant</h3><p>La gestione di una singola raccolta è molto più semplice di quella di più raccolte. Invece di creare più collezioni, si può pensare di assegnare una partizione per ogni tenant per ottenere un isolamento dei dati e una gestione della memoria flessibili. Le prestazioni di ricerca della multi-tenancy orientata alle partizioni sono molto migliori di quelle della multi-tenancy orientata alle collezioni. Tuttavia, si noti che il numero di tenant della collezione non deve superare il numero massimo di partizioni che una collezione può contenere.</p>
<h3 id="Partition-key-based-multi-tenancy" class="common-anchor-header">Multi-tenancy basata su chiavi di partizione</h3><p>Milvus 2.2.9 introduce una nuova funzione chiamata chiave di partizione. Al momento della creazione di una collezione, si nomina un campo tenancy e lo si rende il campo chiave della partizione. Milvus memorizzerà le entità in una partizione in base al valore hash del campo chiave della partizione. Quando si effettuano ricerche su RNA, Milvus cerca solo nella partizione che contiene la chiave di partizione. In questo modo si riduce notevolmente la portata della ricerca e si ottengono prestazioni migliori rispetto a quelle ottenute senza la chiave di partizione.</p>
</div>
<p>Questa strategia elimina il limite del numero massimo di tenant che una collezione Milvus può supportare e semplifica notevolmente la gestione delle risorse perché Milvus gestisce automaticamente le partizioni per voi.</p>
<p>Riassumendo, è possibile utilizzare una o alcune delle strategie multi-tenancy sopra descritte per creare la propria soluzione. La tabella seguente mette a confronto queste strategie in termini di isolamento dei dati, prestazioni di ricerca e numero massimo di tenant.</p>
<table>
<thead>
<tr><th></th><th>Isolamento dei dati</th><th>Prestazioni di ricerca</th><th>Numero massimo di tenant</th><th>Scenari consigliati</th></tr>
</thead>
<tbody>
<tr><td>Orientato al database</td><td>Forte</td><td>Forte</td><td>64</td><td>Per chi ha bisogno di collezioni che variano a seconda dei progetti, particolarmente adatte per l'isolamento dei dati tra i reparti dell'organizzazione.</td></tr>
<tr><td>Una raccolta per tutti</td><td>Debole</td><td>Medio</td><td>N/D</td><td>Per chi ha risorse limitate ed è insensibile all'isolamento dei dati.</td></tr>
<tr><td>Una raccolta per inquilino</td><td>Forte</td><td>Forte</td><td>Meno di 10.000</td><td>Per chi ha meno di 10.000 tenant per cluster.</td></tr>
<tr><td>Una partizione per tenant</td><td>Medio</td><td>Forte</td><td>1,024</td><td>Per chi ha meno di 1.024 tenant per collezione.</td></tr>
<tr><td>Basato su chiavi di partizione</td><td>Medio</td><td>Forte</td><td>10,000,000+</td><td>Per chi prevede un rapido aumento degli affittuari fino a milioni.</td></tr>
</tbody>
</table>
<h2 id="Whats-next" class="common-anchor-header">Cosa c'è dopo<button data-href="#Whats-next" class="anchor-icon" translate="no">
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
    </button></h2><p><a href="/docs/it/manage_databases.md">Gestire</a><a href="/docs/it/schema.md">lo schema dei</a><a href="/docs/it/manage_databases.md">database</a></p>
