---
title: Panoramica dell'API del server NuGet
description: L'API del server NuGet è un set di endpoint HTTP che possono essere usati per scaricare i pacchetti, recuperare i metadati, pubblicare nuovi pacchetti e così via.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237809"
---
# <a name="nuget-server-api"></a>API Server NuGet

L'API del server NuGet è un set di endpoint HTTP che possono essere usati per scaricare i pacchetti, recuperare i metadati, pubblicare nuovi pacchetti ed eseguire la maggior parte delle altre operazioni disponibili nei client NuGet ufficiali.

Questa API viene usata dal client NuGet in Visual Studio, nuget.exe e l'interfaccia della riga di comando di .NET per eseguire operazioni NuGet come [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) , cercare nell'interfaccia utente di Visual Studio e [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md) .

Si noti che in alcuni casi nuget.org presenta requisiti aggiuntivi che non vengono applicati da altre origini di pacchetti. Queste differenze sono documentate dai [protocolli NuGet.org](nuget-protocols.md).

Per una semplice enumerazione e il download delle versioni nuget.exe disponibili, vedere l' [tools.jssull'](tools-json.md) endpoint.

## <a name="service-index"></a>Indice dei servizi

Il punto di ingresso per l'API è un documento JSON in una posizione ben nota. Questo documento è denominato **indice del servizio** . Il percorso dell'indice del servizio per nuget.org è `https://api.nuget.org/v3/index.json` .

Questo documento JSON contiene un elenco di *risorse* che forniscono funzionalità diverse e soddisfano diversi casi d'uso.

I client che supportano l'API devono accettare uno o più di questi URL dell'indice del servizio come mezzo per la connessione alle rispettive origini dei pacchetti.

Per ulteriori informazioni sull'indice del servizio, vedere [le](service-index.md)informazioni di riferimento sulle API.

## <a name="versioning"></a>Controllo delle versioni

L'API è la versione 3 del protocollo HTTP di NuGet. Questo protocollo viene talvolta definito "API V3". Questi documenti di riferimento faranno riferimento a questa versione del protocollo semplicemente come "API".

La versione dello schema dell'indice del servizio è indicata dalla `version` proprietà nell'indice del servizio. L'API impone che la stringa di versione abbia un numero di versione principale di `3` . Quando vengono apportate modifiche non di rilievo allo schema dell'indice del servizio, viene aumentata la versione secondaria della stringa di versione.

I client meno recenti (ad esempio nuget.exe 2. x) non supportano l'API V3 e supportano solo l'API v2 precedente, che non è documentata qui.

L'API NuGet V3 viene denominata come tale perché è il successore dell'API v2, che era il protocollo basato su OData implementato dalla versione 2. x del client NuGet ufficiale. L'API V3 è stata prima supportata dalla versione 3,0 del client NuGet ufficiale ed è ancora la versione più recente del protocollo principale supportata dal client NuGet, 4,0 e su. 

Sono state apportate modifiche al protocollo senza interruzioni dell'API da quando è stato rilasciato per la prima volta.

## <a name="resources-and-schema"></a>Risorse e schema

L' **indice del servizio** descrive un'ampia gamma di risorse. Il set corrente di risorse supportate è il seguente:

Nome risorsa                                                        | Obbligatoria | Descrizione
-------------------------------------------------------------------- | -------- | -----------
[Catalogo](catalog-resource.md)                                       | no       | Record completo di tutti gli eventi del pacchetto.
[PackageBaseAddress](package-base-address-resource.md)               | yes      | Ottenere il contenuto del pacchetto (. nupkg).
[PackageDetailsUriTemplate](package-details-template-resource.md)    | no       | Costruire un URL per accedere a una pagina Web dei dettagli del pacchetto.
[PackagePublish](package-publish-resource.md)                        | yes      | Eseguire il push e l'eliminazione dei pacchetti.
[RegistrationsBaseUrl](registration-base-url-resource.md)            | yes      | Ottenere i metadati del pacchetto.
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | no       | Consente di creare un URL per accedere a una pagina Web di segnalazione di abusi.
[RepositorySignatures](repository-signatures-resource.md)            | no       | Ottiene i certificati utilizzati per la firma del repository.
[SearchAutocompleteService](search-autocomplete-service-resource.md) | no       | Individuare le versioni e gli ID del pacchetto in base alla sottostringa.
[SearchQueryService](search-query-service-resource.md)               | yes      | Filtrare e cercare i pacchetti per parola chiave.
[SymbolPackagePublish](symbol-package-publish-resource.md)           | no       | Eseguire il push dei pacchetti di simboli.

In generale, tutti i dati non binari restituiti da una risorsa API vengono serializzati tramite JSON. Lo schema di risposta restituito da ogni risorsa nell'indice del servizio viene definito singolarmente per tale risorsa. Per ulteriori informazioni su ogni risorsa, vedere gli argomenti elencati in precedenza.

In futuro, con l'evolversi del protocollo, è possibile aggiungere nuove proprietà alle risposte JSON. Affinché il client sia di prova futura, l'implementazione non presuppone che lo schema di risposta sia finale e non possa includere dati aggiuntivi. Tutte le proprietà che l'implementazione non è in grado di comprendere devono essere ignorate.

> [!Note]
> Quando un'origine non implementa `SearchAutocompleteService` alcun comportamento di completamento automatico, deve essere disabilitato correttamente. Quando `ReportAbuseUriTemplate` non viene implementato, il client NuGet ufficiale esegue il fallback all'URL di abusi dei report di NuGet. org (monitorato da [NuGet/Home # 4924](https://github.com/NuGet/Home/issues/4924)). Gli altri client possono scegliere di non visualizzare semplicemente un URL di abuso del report all'utente.

### <a name="undocumented-resources-on-nugetorg"></a>Risorse non documentate in nuget.org

L'indice del servizio V3 in nuget.org include alcune risorse che non sono documentate in precedenza. Esistono alcuni motivi per non documentare una risorsa.

In primo luogo, non vengono documentate le risorse usate come dettaglio di implementazione di nuget.org. La classe `SearchGalleryQueryService` rientra in questa categoria. [Nugetgallery](https://github.com/NuGet/NuGetGallery) usa questa risorsa per delegare alcune query V2 (OData) all'indice di ricerca invece di usare il database. Questa risorsa è stata introdotta per motivi di scalabilità e non è destinata all'uso esterno.

In secondo luogo, non vengono documentate le risorse che non sono mai state fornite in una versione RTM del client ufficiale.
`PackageDisplayMetadataUriTemplate` e `PackageVersionDisplayMetadataUriTemplate` rientrano in questa categoria.

In terzo luogo, non vengono documentate le risorse strettamente associate al protocollo v2, che a sua volta non è documentato intenzionalmente. La `LegacyGallery` risorsa rientra in questa categoria. Questa risorsa consente a un indice del servizio V3 di puntare a un URL di origine V2 corrispondente. Questa risorsa supporta `nuget.exe list` .

Se una risorsa non è documentata in questa sezione, si consiglia *vivamente* di non assumere una dipendenza. È possibile rimuovere o modificare il comportamento di queste risorse non documentate che potrebbero interrompere l'implementazione in modi imprevisti.

## <a name="timestamps"></a>Timestamp

Tutti i timestamp restituiti dall'API sono UTC o altrimenti specificati usando la rappresentazione [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) . 

## <a name="http-methods"></a>Metodi HTTP

Verbo   | Uso
------ | -----------
GET    | Esegue un'operazione di sola lettura, in genere il recupero dei dati.
HEAD   | Recupera le intestazioni della risposta per la `GET` richiesta corrispondente.
PUT    | Crea una risorsa che non esiste o, se esiste, la Aggiorna. Alcune risorse potrebbero non supportare l'aggiornamento.
DELETE | Elimina o rimuove l'elenco di una risorsa.

## <a name="http-status-codes"></a>Codici di stato HTTP

Codice | Descrizione
---- | -----
200  | Success e c'è un corpo della risposta.
201  | Success e la risorsa è stata creata.
202  | Esito positivo, la richiesta è stata accettata, ma alcune operazioni potrebbero essere ancora incomplete e completate in modo asincrono.
204  | Esito positivo, ma non è presente alcun corpo della risposta.
301  | Reindirizzamento permanente.
302  | Reindirizzamento temporaneo.
400  | I parametri nell'URL o nel corpo della richiesta non sono validi.
401  | Le credenziali specificate non sono valide.
403  | L'azione non è consentita in base alle credenziali fornite.
404  | La risorsa richiesta non esiste.
409  | La richiesta è in conflitto con una risorsa esistente.
500  | Si è verificato un errore imprevisto del servizio.
503  | Il servizio è temporaneamente non disponibile.

Qualsiasi `GET` richiesta effettuata a un endpoint API può restituire un reindirizzamento HTTP (301 o 302). I client devono gestire normalmente questi reindirizzamenti osservando l' `Location` intestazione ed eseguendo un successivo `GET` . La documentazione relativa a endpoint specifici non richiama in modo esplicito i reindirizzamenti che possono essere usati.

Nel caso di un codice di stato a livello di 500, il client può implementare un meccanismo di ripetizione dei tentativi ragionevole. Il client NuGet ufficiale ritenta tre volte quando si verifica un codice di stato a livello di 500 o un errore TCP/DNS.

## <a name="http-request-headers"></a>Intestazioni di richiesta HTTP

Nome                     | Descrizione
------------------------ | -----------
X-NuGet-ApiKey           | Obbligatorio per push ed Delete, vedere [ `PackagePublish` Resource](package-publish-resource.md)
X-NuGet-client-version   | **Deprecato** e sostituito da `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Obbligatorio in alcuni casi solo su nuget.org, vedere [protocolli NuGet.org](NuGet-Protocols.md)
X-NuGet-Session-ID       | *Facoltativo* . I client NuGet v 4.7 + identificano le richieste HTTP che fanno parte della stessa sessione client NuGet.

`X-NuGet-Session-Id`Ha un solo valore per tutte le operazioni correlate a un singolo ripristino in `PackageReference` . Per altri scenari, ad esempio il completamento automatico e il ripristino, è possibile che si `packages.config` verifichino diversi ID di sessione a causa del factoring del codice.

## <a name="authentication"></a>Authentication

L'autenticazione viene lasciata all'implementazione di origine del pacchetto da definire. Per nuget.org, solo la `PackagePublish` risorsa richiede l'autenticazione tramite un'intestazione speciale della chiave API. Per informazioni dettagliate, vedere la [ `PackagePublish` risorsa](package-publish-resource.md) .
