---
title: Metadati del pacchetto, API NuGet
description: L'URL di base per la registrazione del pacchetto consente di recuperare i metadati sui pacchetti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 852dca8c70b09d941e844b1f7cd03b38e2192481
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237523"
---
# <a name="package-metadata"></a>Metadati dei pacchetti

È possibile recuperare i metadati relativi ai pacchetti disponibili in un'origine del pacchetto tramite l'API NuGet V3. I metadati possono essere recuperati usando la `RegistrationsBaseUrl` risorsa presente nell' [indice del servizio](service-index.md).

La raccolta dei documenti disponibili in `RegistrationsBaseUrl` viene spesso definita "registrazioni" o "BLOB di registrazione". Il set di documenti in un singolo `RegistrationsBaseUrl` viene definito "hive di registrazione". Un hive di registrazione contiene tutti i metadati relativi a ogni pacchetto disponibile in un'origine del pacchetto.

## <a name="versioning"></a>Controllo delle versioni

`@type`Vengono usati i valori seguenti:

Valore della proprietà @type                     | Note
------------------------------- | -----
RegistrationsBaseUrl            | Versione iniziale
RegistrationsBaseUrl/3.0.0-beta | Alias di `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-RC   | Alias di `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Risposte gzippato
RegistrationsBaseUrl/3.6.0      | Include i pacchetti SemVer 2.0.0

Rappresenta tre hive di registrazione distinti disponibili per diverse versioni client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Queste registrazioni non vengono compresse (ovvero usano un implicito `Content-Encoding: identity` ). I pacchetti SemVer 2.0.0 sono **esclusi** da questo hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Queste registrazioni vengono compresse usando `Content-Encoding: gzip` . I pacchetti SemVer 2.0.0 sono **esclusi** da questo hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Queste registrazioni vengono compresse usando `Content-Encoding: gzip` . I pacchetti SemVer 2.0.0 sono **inclusi** in questo hive.
Per ulteriori informazioni su SemVer 2.0.0, vedere [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà associata ai valori di risorsa menzionati sopra `@type` . Nel documento seguente verrà usato l'URL di base segnaposto `{@id}` .

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi HTTP `GET` e `HEAD` .

## <a name="registration-index"></a>Indice di registrazione

La risorsa di registrazione raggruppa i metadati del pacchetto in base all'ID pacchetto. Non è possibile ottenere dati su più di un ID di pacchetto alla volta. Questa risorsa non fornisce alcun modo per individuare gli ID del pacchetto. Si presuppone invece che il client conosca già l'ID del pacchetto desiderato. I metadati disponibili per ogni versione del pacchetto variano in base all'implementazione del server. I BLOB di registrazione del pacchetto hanno la struttura gerarchica seguente:

- **Index** : il punto di ingresso per i metadati del pacchetto, condiviso da tutti i pacchetti in un'origine con lo stesso ID pacchetto.
- **Pagina** : raggruppamento di versioni del pacchetto. Il numero di versioni del pacchetto in una pagina viene definito dall'implementazione del server.
- **Foglia** : documento specifico per una singola versione del pacchetto.

L'URL dell'indice di registrazione è prevedibile e può essere determinato dal client in base all'ID del pacchetto e al valore della risorsa di registrazione `@id` dall'indice del servizio. Gli URL per le pagine di registrazione e le foglie vengono individuati controllando l'indice di registrazione.

### <a name="registration-pages-and-leaves"></a>Pagine di registrazione e foglie

Sebbene non sia strettamente necessario per un'implementazione del server archiviare le foglie di registrazione in documenti di pagine di registrazione separate, è consigliabile mantenere la memoria sul lato client. Anziché incorporare tutti i fogli di registrazione nell'indice o archiviare immediatamente le foglie nei documenti della pagina, è consigliabile che l'implementazione del server definisca una certa euristica per scegliere tra i due approcci in base al numero di versioni del pacchetto o alle dimensioni cumulative delle foglie del pacchetto.

L'archiviazione di tutte le versioni dei pacchetti (foglie) nell'indice di registrazione salva il numero di richieste HTTP necessarie per recuperare i metadati del pacchetto, ma significa che è necessario scaricare un documento più grande e allocare una maggiore quantità di memoria del client. D'altra parte, se l'implementazione del server archivia immediatamente le foglie di registrazione in documenti di pagine separate, il client deve eseguire più richieste HTTP per ottenere le informazioni necessarie.

L'euristica utilizzata da nuget.org è la seguente: se sono presenti 128 o più versioni di un pacchetto, suddividere le foglie in pagine di dimensioni 64. Se sono presenti meno di 128 versioni, inline tutto lascia nell'indice di registrazione. Si noti che questo significa che i pacchetti con versioni da 65 a 127 avranno due pagine nell'indice, ma entrambe le pagine verranno inline.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametri della richiesta

Nome     | In     | Type    | Obbligatoria | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | yes      | ID del pacchetto, minuscolo

Il `LOWER_ID` valore è l'ID pacchetto desiderato in minuscolo usando le regole implementate da. Metodo NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) .

### <a name="response"></a>Risposta

La risposta è un documento JSON con un oggetto radice con le proprietà seguenti:

Nome  | Type             | Obbligatoria | Note
----- | ---------------- | -------- | -----
count | integer          | yes      | Numero di pagine di registrazione nell'indice
items | matrice di oggetti | yes      | Matrice di pagine di registrazione

Ogni elemento nella matrice dell'oggetto index `items` è un oggetto JSON che rappresenta una pagina di registrazione.

#### <a name="registration-page-object"></a>Oggetto pagina di registrazione

L'oggetto pagina di registrazione trovato nell'indice di registrazione presenta le proprietà seguenti:

Nome   | Type             | Obbligatoria | Note
------ | ---------------- | -------- | -----
@id    | string           | yes      | URL della pagina di registrazione
count  | integer          | yes      | Il numero di fogli di registrazione nella pagina
items  | matrice di oggetti | no       | Matrice di foglie di registrazione e relativi metadati associati
lower  | string           | yes      | Versione SemVer 2.0.0 più bassa nella pagina (inclusivo)
padre | string           | no       | URL dell'indice di registrazione
upper  | string           | yes      | La versione più recente di SemVer 2.0.0 nella pagina (inclusi)

I `lower` `upper` limiti e dell'oggetto pagina sono utili quando sono necessari i metadati per una specifica versione di pagina.
Questi limiti possono essere utilizzati per recuperare l'unica pagina di registrazione necessaria. Le stringhe di versione rispettano le [regole di versione di NuGet](../concepts/package-versioning.md). Le stringhe di versione vengono normalizzate e non includono i metadati di compilazione. Come per tutte le versioni nell'ecosistema NuGet, il confronto delle stringhe di versione viene implementato usando [le regole di precedenza della versione di SemVer 2.0.0](https://semver.org/spec/v2.0.0.html#spec-item-11).

La `parent` proprietà verrà visualizzata solo se l'oggetto pagina di registrazione dispone della `items` Proprietà.

Se la `items` proprietà non è presente nell'oggetto pagina di registrazione, è necessario utilizzare l'URL specificato in `@id` per recuperare i metadati relativi alle singole versioni del pacchetto. La `items` matrice viene talvolta esclusa dall'oggetto pagina come ottimizzazione. Se il numero di versioni di un singolo ID pacchetto è molto grande, il documento dell'indice di registrazione sarà massiccio ed inutile da elaborare per un client che si occupa solo di una versione specifica o di una piccola gamma di versioni.

Si noti che se la `items` proprietà è presente, `@id` non è necessario utilizzare la proprietà, poiché tutti i dati della pagina sono già stati inline nella `items` Proprietà.

Ogni elemento nella matrice dell'oggetto pagina `items` è un oggetto JSON che rappresenta un foglio di registrazione ed è associato ai metadati.

#### <a name="registration-leaf-object-in-a-page"></a>Oggetto foglia di registrazione in una pagina

L'oggetto foglia di registrazione trovato in una pagina di registrazione presenta le proprietà seguenti:

Nome           | Type   | Obbligatoria | Note
-------------- | ------ | -------- | -----
@id            | string | yes      | URL della foglia di registrazione
catalogEntry   | object | yes      | Voce di catalogo contenente i metadati del pacchetto
packageContent | string | yes      | URL del contenuto del pacchetto (. nupkg)

Ogni oggetto foglia di registrazione rappresenta i dati associati a una singola versione del pacchetto.

#### <a name="catalog-entry"></a>Voce di catalogo

La `catalogEntry` proprietà nell'oggetto foglia di registrazione presenta le proprietà seguenti:

Nome                     | Type                       | Obbligatoria | Note
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | yes      | URL del documento utilizzato per produrre questo oggetto
authors                  | Stringa o matrice di stringhe | no       | 
dependencyGroups         | matrice di oggetti           | no       | Dipendenze del pacchetto, raggruppate in base al Framework di destinazione
deprecazione              | object                     | no       | La deprecazione associata al pacchetto
description              | string                     | no       | 
iconUrl                  | string                     | no       | 
id                       | string                     | yes      | ID del pacchetto
licenseUrl               | string                     | no       |
licenseExpression        | string                     | no       | 
disponibili                   | boolean                    | no       | Deve essere considerato come elencato se assente
minClientVersion         | string                     | no       | 
projectUrl               | string                     | no       | 
published                | string                     | no       | Stringa contenente un timestamp ISO 8601 di quando è stato pubblicato il pacchetto
requireLicenseAcceptance | boolean                    | no       | 
riepilogo                  | string                     | no       | 
tags                     | stringa o matrice di stringhe  | no       | 
title                    | string                     | no       | 
version                  | string                     | yes      | Stringa di versione completa dopo la normalizzazione

La `version` Proprietà Package è la stringa di versione completa dopo la normalizzazione. Ciò significa che i dati di compilazione di SemVer 2.0.0 possono essere inclusi qui.

La `dependencyGroups` proprietà è una matrice di oggetti che rappresentano le dipendenze del pacchetto, raggruppate in base al Framework di destinazione. Se il pacchetto non ha dipendenze, la `dependencyGroups` proprietà è mancante, una matrice vuota o la `dependencies` proprietà di tutti i gruppi è vuota o mancante.

Il valore della `licenseExpression` proprietà è conforme alla [sintassi delle espressioni di licenza NuGet](../reference/nuspec.md#license).

> [!Note]
> In nuget.org, il `published` valore viene impostato sull'anno 1900 quando il pacchetto viene riincluso nell'elenco.

#### <a name="package-dependency-group"></a>Gruppo di dipendenze del pacchetto

Ogni oggetto gruppo di dipendenze presenta le proprietà seguenti:

Nome            | Type             | Obbligatoria | Note
--------------- | ---------------- | -------- | -----
targetFramework | string           | no       | Framework di destinazione a cui sono applicabili tali dipendenze.
dipendenze    | matrice di oggetti | no       |

La `targetFramework` stringa usa il formato implementato dalla libreria .NET di NuGet [. Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)di NuGet. Se non `targetFramework` si specifica alcun parametro, il gruppo di dipendenze si applica a tutti i Framework di destinazione.

La `dependencies` proprietà è una matrice di oggetti, ognuno dei quali rappresenta una dipendenza del pacchetto corrente.

#### <a name="package-dependency"></a>Dipendenza del pacchetto

Ogni dipendenza del pacchetto presenta le proprietà seguenti:

Nome         | Type   | Obbligatoria | Note
------------ | ------ | -------- | -----
id           | string | yes      | ID della dipendenza del pacchetto
range        | object | no       | Intervallo di [versioni](../concepts/package-versioning.md#version-ranges) consentite della dipendenza
registrazione | string | no       | URL dell'indice di registrazione per questa dipendenza

Se la `range` proprietà è esclusa o una stringa vuota, il client deve eseguire l'impostazione predefinita sull'intervallo di versioni `(, )` . Ovvero è consentita qualsiasi versione della dipendenza. Il valore di `*` non è consentito per la `range` Proprietà.

#### <a name="package-deprecation"></a>Deprecazione del pacchetto

Ogni deprecazione del pacchetto presenta le proprietà seguenti:

Nome             | Type             | Obbligatoria | Note
---------------- | ---------------- | -------- | -----
motivi          | matrice di stringhe | yes      | Motivi per cui il pacchetto è stato deprecato
message          | string           | no       | Ulteriori dettagli su questa deprecazione
alternatePackage | object           | no       | Il pacchetto alternativo da usare

La `reasons` proprietà deve contenere almeno una stringa e contenere solo le stringhe della tabella seguente:

Motivo       | Descrizione             
------------ | -----------
Legacy       | Il pacchetto non è più gestito
CriticalBugs | Nel pacchetto sono presenti bug che lo rendono non idoneo per l'utilizzo
Altri        | Il pacchetto è deprecato a causa di un motivo non presente nell'elenco

Se la `reasons` proprietà contiene stringhe che non sono del set noto, è necessario ignorarle. Le stringhe non fanno distinzione tra maiuscole e minuscole, pertanto `legacy` devono essere considerate uguali a `Legacy` . Non esiste alcuna restrizione di ordinamento per la matrice, pertanto le stringhe possono essere disposte in qualsiasi ordine arbitrario. Inoltre, se la proprietà contiene solo stringhe che non appartengono al set noto, deve essere considerata come se contenesse solo la stringa "other".

#### <a name="alternate-package"></a>Pacchetto alternativo

L'oggetto pacchetto alternativo presenta le proprietà seguenti:

Nome         | Type   | Obbligatoria | Note
------------ | ------ | -------- | -----
id           | string | yes      | ID del pacchetto alternativo
range        | object | no       | Intervallo di [versione](../concepts/package-versioning.md#version-ranges)consentito o `*` se è consentita una versione

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In questo caso specifico, per l'indice di registrazione è stata applicata la pagina di registrazione, quindi non sono necessarie richieste aggiuntive per recuperare i metadati sulle singole versioni del pacchetto.

## <a name="registration-page"></a>Pagina di registrazione

La pagina di registrazione contiene le foglie di registrazione. L'URL per recuperare una pagina di registrazione è determinato dalla `@id` proprietà nell' [oggetto pagina di registrazione](#registration-page-object) indicato in precedenza. L'URL non deve essere prevedibile e deve essere sempre individuato per mezzo del documento di indice.

> [!Warning]
> In nuget.org, l'URL del documento della pagina di registrazione contiene coincidenza tra il limite inferiore e quello superiore della pagina. Questo presupposto, tuttavia, non deve mai essere effettuato da un client poiché le implementazioni del server sono gratuite per modificare la forma dell'URL purché il documento di indice disponga di un collegamento valido.

Quando la `items` matrice non viene specificata nell'indice di registrazione, una richiesta HTTP Get del `@id` valore restituirà un documento JSON con un oggetto come radice. L'oggetto ha le proprietà seguenti:

Nome   | Type             | Obbligatoria | Note
------ | ---------------- | -------- | -----
@id    | string           | yes      | URL della pagina di registrazione
count  | integer          | yes      | Il numero di fogli di registrazione nella pagina
items  | matrice di oggetti | yes      | Matrice di foglie di registrazione e relativi metadati associati
lower  | string           | yes      | Versione SemVer 2.0.0 più bassa nella pagina (inclusivo)
padre | string           | yes      | URL dell'indice di registrazione
upper  | string           | yes      | La versione più recente di SemVer 2.0.0 nella pagina (inclusi)

La forma degli oggetti foglia di registrazione è identica a quella dell'indice di registrazione [precedente](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Foglia di registrazione

Il foglio di registrazione contiene informazioni su un ID e una versione specifici del pacchetto. I metadati relativi alla versione specifica potrebbero non essere disponibili in questo documento. I metadati del pacchetto devono essere recuperati dall' [indice di registrazione](#registration-index) o dalla pagina di [registrazione](#registration-page) (individuata usando l'indice di registrazione).

L'URL per recuperare un'foglia di registrazione viene ottenuto dalla `@id` proprietà di un oggetto foglia di registrazione in un indice di registrazione o in una pagina di registrazione. Come nel documento della pagina. l'URL non è destinato a essere prevedibile e deve essere sempre individuato tramite l'oggetto pagina di registrazione.

> [!Warning]
> In nuget.org, l'URL del documento foglia di registrazione contiene la versione del pacchetto. Questo presupposto, tuttavia, non deve mai essere effettuato da un client poiché le implementazioni del server sono gratuite per modificare la forma dell'URL, purché il documento padre disponga di un collegamento valido. 

Il foglio di registrazione è un documento JSON con un oggetto radice con le proprietà seguenti:

Nome           | Type    | Obbligatoria | Note
-------------- | ------- | -------- | -----
@id            | string  | yes      | URL della foglia di registrazione
catalogEntry   | string  | no       | URL della voce di catalogo che ha prodotto l'elemento foglia
disponibili         | boolean | no       | Deve essere considerato come elencato se assente
packageContent | string  | no       | URL del contenuto del pacchetto (. nupkg)
published      | string  | no       | Stringa contenente un timestamp ISO 8601 di quando è stato pubblicato il pacchetto
registrazione   | string  | no       | URL dell'indice di registrazione

> [!Note]
> In nuget.org, il `published` valore viene impostato sull'anno 1900 quando il pacchetto viene riincluso nell'elenco.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
