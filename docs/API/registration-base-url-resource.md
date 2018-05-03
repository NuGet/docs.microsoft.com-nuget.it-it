---
title: Metadati del pacchetto, NuGet API
description: L'URL di base di registrazione del pacchetto consente il recupero di metadati sui pacchetti.
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 50064e1450232e9cdedcc042a09c08860f802e76
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
---
# <a name="package-metadata"></a>Metadati del pacchetto

È possibile recuperare i metadati relativi ai pacchetti disponibili su un'origine del pacchetto tramite l'API di NuGet V3. Questi metadati possono essere recuperati tramite il `RegistrationsBaseUrl` risorse, vedere il [indice servizio](service-index.md).

La raccolta dei documenti in `RegistrationsBaseUrl` vengono spesso denominati "registrazioni" o "registrazione BLOB". Il set di documenti in un unico `RegistrationsBaseUrl` viene definito un hive"registrazione". Un hive registrazione contiene tutti i metadati relativi a tutti i pacchetti disponibili su un'origine pacchetto.

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                     | Note
------------------------------- | -----
RegistrationsBaseUrl            | La versione iniziale
RegistrationsBaseUrl/3.0.0-beta | Alias di `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias di `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Risposte compresso con gzip
RegistrationsBaseUrl/3.6.0      | Include pacchetti SemVer 2.0.0

Questo rappresenta tre hive registrazione distinct è disponibili per le diverse versioni di client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Queste registrazioni non vengono compressi (vale a dire che utilizzano un implicita `Content-Encoding: identity`). I pacchetti SemVer 2.0.0 sono **esclusi** dall'hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Queste registrazioni vengono compressi utilizzando `Content-Encoding: gzip`. I pacchetti SemVer 2.0.0 sono **esclusi** dall'hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Queste registrazioni vengono compressi utilizzando `Content-Encoding: gzip`. I pacchetti SemVer 2.0.0 sono **incluso** in questo hive.
Per ulteriori informazioni su SemVer 2.0.0, vedere [supporto SemVer 2.0.0 per nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore di `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valori. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.

## <a name="registration-index"></a>Indice di registrazione

I gruppi di risorse di registrazione del pacchetto dei metadati dall'ID del pacchetto. Non è possibile ottenere i dati relativi a più di un ID di pacchetto alla volta. Questa risorsa non consente di individuare gli ID di pacchetto. Invece il client si presuppone che conosce l'ID pacchetto desiderato. I metadati disponibili relativi a ogni versione del pacchetto variano dall'implementazione di server. I BLOB di registrazione del pacchetto hanno una struttura gerarchica seguente:

- **Indice**: il punto di ingresso per i metadati del pacchetto, condivisi da tutti i pacchetti su un'origine con lo stesso ID di pacchetto.
- **Pagina**: un raggruppamento di versioni del pacchetto. Il numero di versioni del pacchetto in una pagina viene definito dall'implementazione di server.
- **Foglia**: un documento specifico per una versione singolo pacchetto.

L'URL dell'indice registrazione prevedibile e può essere determinato dal client di cui è assegnato un ID pacchetto e la risorsa di registrazione `@id` valore dall'indice di servizio. Gli URL per le pagine di registrazione e le foglie vengono individuati tramite l'analisi dell'indice di registrazione.

### <a name="registration-pages-and-leaves"></a>Lascia e pagine di registrazione

Sebbene non sia strettamente è necessario per un'implementazione di server archiviare foglie di registrazione di un nei documenti di pagina di registrazione separati, è consigliabile conservare la memoria sul lato client. Anziché l'inlining di tutti registrazione lascia in corrispondenza dell'indice o l'archiviazione immediatamente lascia nei documenti di pagina, è consigliabile che l'implementazione del server di definire un approccio euristico per scegliere tra i due approcci in base al numero di versioni del pacchetto o lascia la dimensione complessiva del pacchetto.

L'archiviazione di tutte le versioni di pacchetto (foglie) nei salvataggi di indice di registrazione per il numero di richieste HTTP necessaria per l'operazione di recupero dei metadati del pacchetto, ma indica che è necessario scaricare un documento più grande e deve essere allocata più memoria del client. D'altra parte, se l'implementazione del server archivia immediatamente registrazione lascia nei documenti di una pagina separata, il client deve eseguire più richieste HTTP per ottenere le informazioni che necessarie.

L'euristica di nuget.org viene utilizzato come segue: se sono presenti 128 o più versioni di un pacchetto, suddividere le foglie in pagine di dimensioni di 64. Se sono disponibili versioni meno di 128, inline tutti lascia nell'indice della registrazione.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametri della richiesta

nome     | In     | Tipo    | Obbligatorio | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | stringa  | sì      | L'ID del pacchetto, minuscola

Il `LOWER_ID` valore è l'ID del pacchetto desiderato minuscola usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.

### <a name="response"></a>Risposta

La risposta è un documento JSON che include un oggetto principale con le proprietà seguenti:

nome  | Tipo             | Obbligatorio | Note
----- | ---------------- | -------- | -----
count | numero intero          | sì      | Il numero di pagine di registrazione nell'indice
Elementi | Matrice di oggetti | sì      | Matrice di pagine di registrazione

Ogni elemento nell'oggetto indice `items` matrice è un oggetto JSON che rappresenta una pagina di registrazione.

#### <a name="registration-page-object"></a>Oggetto pagina registrazione

Oggetto della pagina di registrazione trovato nell'indice della registrazione dispone delle proprietà seguenti:

nome   | Tipo             | Obbligatorio | Note
------ | ---------------- | -------- | -----
@id    | stringa           | sì      | L'URL alla pagina di registrazione
count  | numero intero          | sì      | Il numero di registrazione lascia nella pagina
Elementi  | Matrice di oggetti | No       | La matrice di registrazione lascia e i relativi metadati associati
Inferiore  | stringa           | sì      | La versione meno recente SemVer 2.0.0 nella pagina (inclusiva)
Elemento padre | stringa           | No       | L'URL per l'indice di registrazione
superiore  | stringa           | sì      | La versione più recente SemVer 2.0.0 nella pagina (inclusiva)

Il `lower` e `upper` limiti dell'oggetto di pagina sono utili quando i metadati per una versione di pagina specifica sono necessari.
Questi limiti possono essere usati per recuperare la pagina di registrazione solo necessita. Rispettino le stringhe di versione [regole per la versione NuGet](../reference/package-versioning.md). Le stringhe di versione sono normalizzate e non includono i metadati di compilazione. Come con tutte le versioni all'interno dell'ecosistema di NuGet, confronto tra stringhe di versione viene implementato utilizzando [le regole di precedenza versione SemVer 2.0.0's](http://semver.org/spec/v2.0.0.html#spec-item-11).

Il `parent` proprietà verrà visualizzata solo se l'oggetto di pagina di registrazione ha il `items` proprietà.

Se il `items` proprietà non è presente nell'oggetto della pagina di registrazione, l'URL specificato nella `@id` deve essere usato per recuperare i metadati relativi a versioni singolo pacchetto. Il `items` matrice talvolta viene escluso dall'oggetto page per motivi di ottimizzazione. Se il numero di versioni di un ID pacchetto singolo è molto grande, il documento di indicizzazione di registrazione sarà notevole e dispendiosa al processo per un client che può interessare solo su una versione specifica o un breve intervallo di versioni.

Si noti che se il `items` proprietà è presente, il `@id` proprietà non è necessario utilizzare, perché tutti i dati di pagina è già resa inline nel `items` proprietà.

Ogni elemento nell'oggetto pagina `items` matrice è un oggetto JSON che rappresenta un nodo foglia di registrazione e sono associati metadati.

#### <a name="registration-leaf-object-in-a-page"></a>Oggetto foglia di registrazione in una pagina

L'oggetto foglia registrazione trovato in una pagina di registrazione ha le proprietà seguenti:

nome           | Tipo   | Obbligatorio | Note
-------------- | ------ | -------- | -----
@id            | stringa | sì      | L'URL per la foglia di registrazione
catalogEntry   | object | sì      | La voce del catalogo che contiene i metadati del pacchetto
packageContent | stringa | sì      | L'URL per il contenuto del pacchetto (.nupkg)

Ogni oggetto foglia registrazione rappresenta i dati associati a una versione singolo pacchetto.

#### <a name="catalog-entry"></a>Voce di catalogo

Il `catalogEntry` proprietà nell'oggetto foglia registrazione presenta le seguenti proprietà:

nome                     | Tipo                       | Obbligatorio | Note
------------------------ | -------------------------- | -------- | -----
@id                      | stringa                     | sì      | L'URL documento utilizzato per produrre questo oggetto
authors                  | stringa o matrice di stringhe | No       | 
dependencyGroups         | Matrice di oggetti           | No       | Le dipendenze del pacchetto, raggruppati per framework di destinazione
Descrizione              | stringa                     | No       | 
iconUrl                  | stringa                     | No       | 
ID                       | stringa                     | sì      | L'ID del pacchetto
licenseUrl               | stringa                     | No       | 
disponibili                   | boolean                    | No       | Deve essere considerato come se assente, elencati
minClientVersion         | stringa                     | No       | 
projectUrl               | stringa                     | No       | 
Pubblicato                | stringa                     | No       | Stringa contenente un timestamp ISO 8601 di quando il pacchetto è stato pubblicato
requireLicenseAcceptance | boolean                    | No       | 
summary                  | stringa                     | No       | 
tag                     | stringa o matrice di stringhe  | No       | 
title                    | stringa                     | No       | 
version                  | stringa                     | sì      | La versione del pacchetto

Il `dependencyGroups` proprietà è una matrice di oggetti che rappresentano le dipendenze del pacchetto, raggruppati in base al framework di destinazione. Se il pacchetto senza dipendenze, il `dependencyGroups` proprietà manca, una matrice vuota, o `dependencies` proprietà di tutti i gruppi è vuoto o mancante.

#### <a name="package-dependency-group"></a>Gruppo di dipendenze di pacchetto

Ogni oggetto di dipendenza gruppo dispone delle proprietà seguenti:

nome            | Tipo             | Obbligatorio | Note
--------------- | ---------------- | -------- | -----
targetFramework | stringa           | No       | Il framework di destinazione che queste dipendenze sono applicabili a
dependencies    | Matrice di oggetti | No       |

Il `targetFramework` stringa Usa il formato implementato dalla libreria .NET di NuGet [NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/). Se non `targetFramework` viene specificato, il gruppo di dipendenze si applica a tutti i framework di destinazione.

Il `dependencies` proprietà è una matrice di oggetti, ognuno dei quali rappresenta una dipendenza pacchetto del pacchetto corrente.

#### <a name="package-dependency"></a>Dipendenze di pacchetto

Dipendenza ogni pacchetto ha le proprietà seguenti:

nome         | Tipo   | Obbligatorio | Note
------------ | ------ | -------- | -----
ID           | stringa | sì      | L'ID della dipendenza pacchetto
range        | object | No       | Consentiti [intervallo di versioni](../reference/package-versioning.md#version-ranges-and-wildcards) della dipendenza
registrazione | stringa | No       | L'URL per l'indice di registrazione per questa dipendenza

Se il `range` è esclusa proprietà o una stringa vuota, il client deve essere predefinito per l'intervallo di versioni `(, )`. Ovvero, qualsiasi versione della dipendenza è consentita.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In questo caso specifico, l'indice di registrazione ha una pagina di registrazione inline, non esistono richieste aggiuntive sono necessari per recuperare i metadati relativi a versioni singolo pacchetto.

## <a name="registration-page"></a>Pagina di registrazione

La pagina di registrazione contiene lascia la registrazione. L'URL per recuperare una pagina di registrazione è determinato dal `@id` proprietà il [oggetto pagina registrazione](#registration-page-object) indicato in precedenza.

Quando il `items` di matrice non viene fornita nell'indice della registrazione, richiesta di una richiesta GET HTTP di `@id` valore verrà restituito un documento JSON che dispone di un oggetto come radice. L'oggetto ha le proprietà seguenti:

nome   | Tipo             | Obbligatorio | Note
------ | ---------------- | -------- | -----
@id    | stringa           | sì      | L'URL alla pagina di registrazione
count  | numero intero          | sì      | Il numero di registrazione lascia nella pagina
Elementi  | Matrice di oggetti | sì      | La matrice di registrazione lascia e i relativi metadati associati
Inferiore  | stringa           | sì      | La versione meno recente SemVer 2.0.0 nella pagina (inclusiva)
Elemento padre | stringa           | sì      | L'URL per l'indice di registrazione
superiore  | stringa           | sì      | La versione più recente SemVer 2.0.0 nella pagina (inclusiva)

La forma degli oggetti foglia registrazione è uguale a quello dell'indice di registrazione [sopra](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Foglia di registrazione

Foglia registrazione contiene informazioni su un ID pacchetto specifico e una versione. I metadati sulla versione specifica potrebbero non essere disponibili in questo documento. Metadati del pacchetto devono essere recuperati dal [indice registrazione](#registration-index) o [pagina di registrazione](#registration-page) (che viene individuato tramite l'indice di registrazione).

L'URL per recuperare un nodo foglia di registrazione viene ottenuta la `@id` proprietà di un oggetto foglia di registrazione in un indice di registrazione o pagina di registrazione.

La foglia di registrazione è un documento JSON con un oggetto di primo livello con le proprietà seguenti:

nome           | Tipo    | Obbligatorio | Note
-------------- | ------- | -------- | -----
@id            | stringa  | sì      | L'URL per la foglia di registrazione
catalogEntry   | stringa  | No       | L'URL per la voce del catalogo che ha generato questi foglia
disponibili         | boolean | No       | Deve essere considerato come se assente, elencati
packageContent | stringa  | No       | L'URL per il contenuto del pacchetto (.nupkg)
Pubblicato      | stringa  | No       | Stringa contenente un timestamp ISO 8601 di quando il pacchetto è stato pubblicato
registrazione   | stringa  | No       | L'URL per l'indice di registrazione

> [!Note]
> In nuget.org, il `published` è impostato su anni 1900 quando il pacchetto è incluso nell'elenco.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
