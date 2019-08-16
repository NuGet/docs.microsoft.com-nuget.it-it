---
title: Metadati del pacchetto, API NuGet
description: L'URL di base per la registrazione del pacchetto consente di recuperare i metadati sui pacchetti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488308"
---
# <a name="package-metadata"></a>Metadati dei pacchetti

È possibile recuperare i metadati relativi ai pacchetti disponibili in un'origine del pacchetto tramite l'API NuGet V3. I metadati possono essere recuperati usando la `RegistrationsBaseUrl` risorsa presente nell' [indice del servizio](service-index.md).

La raccolta dei documenti disponibili in `RegistrationsBaseUrl` viene spesso definita "registrazioni" o "BLOB di registrazione". Il set di documenti in un singolo `RegistrationsBaseUrl` viene definito "hive di registrazione". Un hive di registrazione contiene tutti i metadati relativi a ogni pacchetto disponibile in un'origine del pacchetto.

## <a name="versioning"></a>Controllo delle versioni

Vengono usati `@type` i valori seguenti:

Valore di @type                     | Note
------------------------------- | -----
RegistrationsBaseUrl            | Versione iniziale
RegistrationsBaseUrl/3.0.0-beta | Alias di`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | Alias di`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Risposte gzippato
RegistrationsBaseUrl/3.6.0      | Include i pacchetti SemVer 2.0.0

Rappresenta tre hive di registrazione distinti disponibili per diverse versioni client.

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

Queste registrazioni non vengono compresse (ovvero usano un implicito `Content-Encoding: identity`). I pacchetti SemVer 2.0.0 sono esclusi da questo hive.

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

Queste registrazioni vengono compresse usando `Content-Encoding: gzip`. I pacchetti SemVer 2.0.0 sono esclusi da questo hive.

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

Queste registrazioni vengono compresse usando `Content-Encoding: gzip`. I pacchetti SemVer 2.0.0 sono **inclusi** in questo hive.
Per ulteriori informazioni su SemVer 2.0.0, vedere [supporto di SemVer 2.0.0 per NuGet.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29).

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà associata ai valori di risorsa `@type` menzionati sopra. Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.

## <a name="registration-index"></a>Indice di registrazione

La risorsa di registrazione raggruppa i metadati del pacchetto in base all'ID pacchetto. Non è possibile ottenere dati su più di un ID di pacchetto alla volta. Questa risorsa non fornisce alcun modo per individuare gli ID del pacchetto. Si presuppone invece che il client conosca già l'ID del pacchetto desiderato. I metadati disponibili per ogni versione del pacchetto variano in base all'implementazione del server. I BLOB di registrazione del pacchetto hanno la struttura gerarchica seguente:

- **Index**: il punto di ingresso per i metadati del pacchetto, condiviso da tutti i pacchetti in un'origine con lo stesso ID pacchetto.
- **Pagina**: raggruppamento di versioni del pacchetto. Il numero di versioni del pacchetto in una pagina viene definito dall'implementazione del server.
- **Foglia**: documento specifico per una singola versione del pacchetto.

L'URL dell'indice di registrazione è prevedibile e può essere determinato dal client in base all'ID del pacchetto e al `@id` valore della risorsa di registrazione dall'indice del servizio. Gli URL per le pagine di registrazione e le foglie vengono individuati controllando l'indice di registrazione.

### <a name="registration-pages-and-leaves"></a>Pagine di registrazione e foglie

Sebbene non sia strettamente necessario per un'implementazione del server archiviare le foglie di registrazione in documenti di pagine di registrazione separate, è consigliabile mantenere la memoria sul lato client. Anziché incorporare tutti i fogli di registrazione nell'indice o archiviare immediatamente le foglie nei documenti della pagina, è consigliabile che l'implementazione del server definisca una certa euristica per scegliere tra i due approcci in base al numero di versioni del pacchetto o dimensioni cumulative delle foglie del pacchetto.

L'archiviazione di tutte le versioni dei pacchetti (foglie) nell'indice di registrazione salva il numero di richieste HTTP necessarie per recuperare i metadati del pacchetto, ma significa che è necessario scaricare un documento più grande e allocare una maggiore quantità di memoria del client. D'altra parte, se l'implementazione del server archivia immediatamente le foglie di registrazione in documenti di pagine separate, il client deve eseguire più richieste HTTP per ottenere le informazioni necessarie.

L'euristica utilizzata da nuget.org è la seguente: se sono presenti 128 o più versioni di un pacchetto, suddividere le foglie in pagine di dimensioni 64. Se sono presenti meno di 128 versioni, inline tutto lascia nell'indice di registrazione.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametri della richiesta

Name     | In     | Type    | Obbligatoria | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | sì      | ID del pacchetto, minuscolo

Il `LOWER_ID` valore è l'ID pacchetto desiderato in minuscolo usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.

### <a name="response"></a>Risposta

La risposta è un documento JSON con un oggetto radice con le proprietà seguenti:

Name  | Type             | Obbligatoria | Note
----- | ---------------- | -------- | -----
count | integer          | sì      | Numero di pagine di registrazione nell'indice
elementi | matrice di oggetti | sì      | Matrice di pagine di registrazione

Ogni elemento nella `items` matrice dell'oggetto index è un oggetto JSON che rappresenta una pagina di registrazione.

#### <a name="registration-page-object"></a>Oggetto pagina di registrazione

L'oggetto pagina di registrazione trovato nell'indice di registrazione presenta le proprietà seguenti:

Name   | Type             | Obbligatoria | Note
------ | ---------------- | -------- | -----
@id    | string           | sì      | URL della pagina di registrazione
count  | integer          | sì      | Il numero di fogli di registrazione nella pagina
elementi  | matrice di oggetti | no       | Matrice di foglie di registrazione e relativi metadati associati
inferiore  | string           | sì      | Versione SemVer 2.0.0 più bassa nella pagina (inclusivo)
padre | string           | no       | URL dell'indice di registrazione
superiore  | string           | sì      | La versione più recente di SemVer 2.0.0 nella pagina (inclusi)

I `lower` limiti `upper` e dell'oggetto pagina sono utili quando sono necessari i metadati per una specifica versione di pagina.
Questi limiti possono essere utilizzati per recuperare l'unica pagina di registrazione necessaria. Le stringhe di versione rispettano le [regole di versione di NuGet](../concepts/package-versioning.md). Le stringhe di versione vengono normalizzate e non includono i metadati di compilazione. Come per tutte le versioni nell'ecosistema NuGet, il confronto delle stringhe di versione viene implementato usando [le regole di precedenza della versione di SemVer 2.0.0](http://semver.org/spec/v2.0.0.html#spec-item-11).

La `parent` proprietà verrà visualizzata solo se l'oggetto pagina di registrazione dispone `items` della proprietà.

Se la `items` proprietà non è presente nell'oggetto pagina di registrazione, è `@id` necessario utilizzare l'URL specificato in per recuperare i metadati relativi alle singole versioni del pacchetto. La `items` matrice viene talvolta esclusa dall'oggetto pagina come ottimizzazione. Se il numero di versioni di un singolo ID pacchetto è molto grande, il documento dell'indice di registrazione sarà massiccio ed inutile da elaborare per un client che si occupa solo di una versione specifica o di una piccola gamma di versioni.

Si noti che se `items` la proprietà è presente, `@id` non è necessario utilizzare la proprietà, poiché tutti i dati della pagina sono già stati inline nella `items` proprietà.

Ogni elemento nella `items` matrice dell'oggetto pagina è un oggetto JSON che rappresenta un foglio di registrazione ed è associato ai metadati.

#### <a name="registration-leaf-object-in-a-page"></a>Oggetto foglia di registrazione in una pagina

L'oggetto foglia di registrazione trovato in una pagina di registrazione presenta le proprietà seguenti:

Name           | Type   | Obbligatoria | Note
-------------- | ------ | -------- | -----
@id            | string | sì      | URL della foglia di registrazione
catalogEntry   | object | sì      | Voce di catalogo contenente i metadati del pacchetto
packageContent | string | sì      | URL del contenuto del pacchetto (. nupkg)

Ogni oggetto foglia di registrazione rappresenta i dati associati a una singola versione del pacchetto.

#### <a name="catalog-entry"></a>Voce di catalogo

La `catalogEntry` proprietà nell'oggetto foglia di registrazione presenta le proprietà seguenti:

Name                     | Type                       | Obbligatoria | Note
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | sì      | URL del documento utilizzato per produrre questo oggetto
authors                  | stringa o matrice di stringhe | no       | 
dependencyGroups         | matrice di oggetti           | no       | Dipendenze del pacchetto, raggruppate in base al Framework di destinazione
deprecazione              | object                     | no       | La deprecazione associata al pacchetto
description              | string                     | no       | 
iconUrl                  | string                     | no       | 
id                       | string                     | sì      | ID del pacchetto
licenseUrl               | string                     | no       |
licenseExpression        | string                     | no       | 
disponibili                   | boolean                    | no       | Deve essere considerato come elencato se assente
minClientVersion         | string                     | no       | 
projectUrl               | string                     | no       | 
Pubblicato                | string                     | no       | Stringa contenente un timestamp ISO 8601 di quando è stato pubblicato il pacchetto
requireLicenseAcceptance | boolean                    | no       | 
summary                  | string                     | no       | 
tags                     | stringa o matrice di stringhe  | no       | 
title                    | string                     | no       | 
version                  | string                     | sì      | Stringa di versione completa dopo la normalizzazione

La proprietà `version` Package è la stringa di versione completa dopo la normalizzazione. Ciò significa che i dati di compilazione di SemVer 2.0.0 possono essere inclusi qui.

La `dependencyGroups` proprietà è una matrice di oggetti che rappresentano le dipendenze del pacchetto, raggruppate in base al Framework di destinazione. Se il pacchetto non ha dipendenze, `dependencyGroups` la proprietà è mancante, una matrice vuota o la `dependencies` proprietà di tutti i gruppi è vuota o mancante.

Il valore della `licenseExpression` proprietà è conforme alla [sintassi delle espressioni di licenza NuGet](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license).

#### <a name="package-dependency-group"></a>Gruppo di dipendenze del pacchetto

Ogni oggetto gruppo di dipendenze presenta le proprietà seguenti:

Name            | Type             | Obbligatoria | Note
--------------- | ---------------- | -------- | -----
targetFramework | string           | no       | Framework di destinazione a cui sono applicabili tali dipendenze.
dipendenze    | matrice di oggetti | no       |

La `targetFramework` stringa usa il formato implementato dalla libreria .NET di NuGet [. Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)di NuGet. Se non `targetFramework` si specifica alcun parametro, il gruppo di dipendenze si applica a tutti i Framework di destinazione.

La `dependencies` proprietà è una matrice di oggetti, ognuno dei quali rappresenta una dipendenza del pacchetto corrente.

#### <a name="package-dependency"></a>Dipendenza del pacchetto

Ogni dipendenza del pacchetto presenta le proprietà seguenti:

NOME         | Type   | Obbligatoria | Note
------------ | ------ | -------- | -----
id           | string | sì      | ID della dipendenza del pacchetto
range        | object | no       | Intervallo di [versioni](../concepts/package-versioning.md#version-ranges-and-wildcards) consentite della dipendenza
registrazione | string | no       | URL dell'indice di registrazione per questa dipendenza

Se la `range` proprietà è esclusa o una stringa vuota, il client deve eseguire l'impostazione predefinita `(, )`sull'intervallo di versioni. Ovvero è consentita qualsiasi versione della dipendenza.

#### <a name="package-deprecation"></a>Deprecazione pacchetto

Ogni deprecazione del pacchetto presenta le proprietà seguenti:

NOME             | Type             | Obbligatoria | Note
---------------- | ---------------- | -------- | -----
motivi          | matrice di stringhe | sì      | Motivi per cui il pacchetto è stato deprecato
message          | string           | no       | Ulteriori dettagli su questa deprecazione
alternatePackage | object           | no       | Dipendenza del pacchetto che deve essere utilizzata

La `reasons` proprietà deve contenere almeno una stringa e contenere solo le stringhe della tabella seguente:

`Reason`       | DESCRIZIONE             
------------ | -----------
Legacy       | Il pacchetto non è più gestito
CriticalBugs | Nel pacchetto sono presenti bug che lo rendono non idoneo per l'utilizzo
Altro        | Il pacchetto è deprecato a causa di un motivo non presente nell'elenco

Se la `reasons` proprietà contiene stringhe che non sono del set noto, è necessario ignorarle. Le stringhe non fanno distinzione tra maiuscole e `legacy` minuscole, pertanto devono essere `Legacy`considerate uguali a. Non esiste alcuna restrizione di ordinamento per la matrice, pertanto le stringhe possono essere disposte in qualsiasi ordine arbitrario. Inoltre, se la proprietà contiene solo stringhe che non appartengono al set noto, deve essere considerata come se contenesse solo la stringa "other".

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

In questo caso specifico, per l'indice di registrazione è stata applicata la pagina di registrazione, quindi non sono necessarie richieste aggiuntive per recuperare i metadati sulle singole versioni del pacchetto.

## <a name="registration-page"></a>Pagina di registrazione

La pagina di registrazione contiene le foglie di registrazione. L'URL per recuperare una pagina di registrazione è determinato dalla `@id` proprietà nell' [oggetto pagina di registrazione](#registration-page-object) indicato in precedenza.

Quando la `items` matrice non viene specificata nell'indice di registrazione, una richiesta HTTP Get `@id` del valore restituirà un documento JSON con un oggetto come radice. L'oggetto ha le proprietà seguenti:

Name   | Type             | Obbligatoria | Note
------ | ---------------- | -------- | -----
@id    | string           | sì      | URL della pagina di registrazione
count  | integer          | sì      | Il numero di fogli di registrazione nella pagina
elementi  | matrice di oggetti | sì      | Matrice di foglie di registrazione e relativi metadati associati
inferiore  | string           | sì      | Versione SemVer 2.0.0 più bassa nella pagina (inclusivo)
padre | string           | sì      | URL dell'indice di registrazione
superiore  | string           | sì      | La versione più recente di SemVer 2.0.0 nella pagina (inclusi)

La forma degli oggetti foglia di registrazione è identica a quella dell'indice di registrazione [precedente](#registration-leaf-object-in-a-page).

## <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>Foglia di registrazione

Il foglio di registrazione contiene informazioni su un ID e una versione specifici del pacchetto. I metadati relativi alla versione specifica potrebbero non essere disponibili in questo documento. I metadati del pacchetto devono essere recuperati dall' [indice di registrazione](#registration-index) o dalla pagina di [registrazione](#registration-page) (individuata usando l'indice di registrazione).

L'URL per recuperare un'foglia di registrazione viene ottenuto dalla `@id` proprietà di un oggetto foglia di registrazione in un indice di registrazione o in una pagina di registrazione.

Il foglio di registrazione è un documento JSON con un oggetto radice con le proprietà seguenti:

Name           | Type    | Obbligatoria | Note
-------------- | ------- | -------- | -----
@id            | string  | sì      | URL della foglia di registrazione
catalogEntry   | string  | no       | URL della voce di catalogo che ha prodotto l'elemento foglia
disponibili         | boolean | no       | Deve essere considerato come elencato se assente
packageContent | string  | no       | URL del contenuto del pacchetto (. nupkg)
Pubblicato      | string  | no       | Stringa contenente un timestamp ISO 8601 di quando è stato pubblicato il pacchetto
registrazione   | string  | no       | URL dell'indice di registrazione

> [!Note]
> In NuGet.org, il `published` valore viene impostato sull'anno 1900 quando il pacchetto viene riincluso nell'elenco.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
