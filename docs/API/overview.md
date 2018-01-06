---
title: Panoramica, NuGet API | Documenti Microsoft
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 8c81f1ac-18c7-44d1-b2e3-584fe85dee6f
description: "L'API di NuGet è un set di endpoint HTTP che può essere usato per scaricare i pacchetti, recuperare metadati, la pubblicazione di nuovi pacchetti e così via."
keywords: API V3 NuGet, API V2 NuGet, NuGet JSON, API di registrazione NuGet, contenitore flat API NuGet, NuGet nupkg API, l'API dei metadati di NuGet, API di ricerca NuGet, push NuGet API, NuGe pubblicare API NuGet eliminare API, esclusione di NuGet API, il protocollo di NuGet
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 05ed17f12f413d29d97a253d7d55f154d4910834
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="nuget-api"></a>API NuGet

L'API di NuGet è un set di endpoint HTTP che può essere utilizzato per scaricare i pacchetti, recuperare metadati, la pubblicazione di nuovi pacchetti ed eseguire la maggior parte delle altre operazioni disponibili nei client NuGet ufficiale.

Questa API viene usata dal client NuGet in Visual Studio, nuget.exe e l'interfaccia CLI .NET per eseguire operazioni di NuGet come [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), ricerca nell'interfaccia utente di Visual Studio, e [ `nuget.exe push` ](../tools/cli-ref-push.md).

Si noti in alcuni casi, nuget.org prevede requisiti aggiuntivi che vengono applicati da altre origini pacchetto. Queste differenze sono documentate in base il [nuget.org protocolli](nuget-protocols.md).

## <a name="service-index"></a>Indice del servizio

Il punto di ingresso per l'API è un documento JSON in un percorso noto. Questo documento viene definito il **indice servizio**.
È la posizione dell'indice del servizio per nuget.org `https://api.nuget.org/v3/index.json`.

Questo documento JSON contiene un elenco di *risorse* che forniscono funzionalità diversi e soddisfare i diversi casi d'uso.

I client che supportano l'API devono accettare uno o più di questi URL del servizio di indice, come i mezzi per la connessione alle origini rispettivi pacchetti.

Per ulteriori informazioni sull'indice di servizio, vedere [il riferimento all'API](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

L'API è versione 3 del protocollo HTTP di NuGet. Questo protocollo è talvolta detta "API V3." Questi documenti di riferimento farà riferimento a questa versione del protocollo semplicemente come "API".

La versione dello schema di indice del servizio è indicata dal `version` proprietà nell'indice di servizio. L'API richiede che la stringa di versione è un numero di versione principale `3`. Al momento non modifiche allo schema di indice del servizio, versione secondaria della stringa di versione verrà aumentato.

Client meno recenti (ad esempio nuget.exe 2. x) non supportano l'API V3 e supportano solo l'API di V2 precedente, che non è documentata.

L'API di V3 NuGet è denominato in quanto tali perché è il successore dell'API V2, di cui è stato il protocollo basato su OData implementato dalla versione 2. x del client NuGet ufficiale. L'API V3 inizialmente supportato dalla versione 3.0 del client NuGet ufficiale ed è ancora la versione più recente principali protocollo supportata dal client NuGet, 4.0 e in. 

Non sostanziale protocollo modifica apportata all'API rispetto alla prima versione.

## <a name="resources-and-schema"></a>Risorse e dello schema

Il **indice servizio** descrive una serie di risorse. Il set corrente di risorse supportati sono i seguenti:

Nome della risorsa                                                          | Obbligatorio | Descrizione
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | sì      | Push ed eliminare o esclusione di pacchetti.
[`SearchQueryService`](search-query-service-resource.md)               | sì      | Filtrare e cercare i pacchetti dalla parola chiave.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | sì      | Ottenere i metadati del pacchetto.
[`PackageBaseAddress`](package-base-address-resource.md)               | sì      | Ottenere il contenuto del pacchetto (.nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | No       | Individuare gli ID di pacchetto e le versioni con sottostringa.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | No       | Costruire un URL per accedere a una pagina web "per segnalare abusi".
[`Catalog`](catalog-resource.md)                                       | No       | Record completo di tutti gli eventi del pacchetto.

In generale, tutti i dati binari non restituiti da una risorsa API vengono serializzati usando JSON. Lo schema di risposta restituito da ogni risorsa in corrispondenza dell'indice del servizio è definito singolarmente per tale risorsa. Per ulteriori informazioni sulle singole risorse, vedere gli argomenti elencati in precedenza.

> [!Note]
> Quando un'origine non implementa `SearchAutocompleteService` qualsiasi comportamento di completamento automatico deve essere disabilitata normalmente. Quando `ReportAbuseUriTemplate` non è implementato, l'ufficiale NuGet client esegue il fallback a di nuget.org segnalare abusi URL (rilevati da [NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924)). Altri client possono decidere di semplicemente non visualizzare un URL di evitare eventuali abusi report all'utente.

## <a name="timestamps"></a>Timestamp

Timestamp tutte restituito dall'API sono ora UTC o sono specificate usando [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) rappresentazione. 

## <a name="http-methods"></a>Metodi HTTP

Verbo   | Usa
------ | -----------
GET    | Esegue un'operazione di sola lettura, in genere il recupero dei dati.
HEAD   | Recupera le intestazioni di risposta per il corrispondente `GET` richiesta.
PUT    | Crea una risorsa che non esiste o, se esiste, viene aggiornato. Alcune risorse potrebbero non supportare l'aggiornamento.
DELETE | Elimina o unlists una risorsa.

## <a name="http-status-codes"></a>Codici di stato HTTP

Codice | Descrizione
---- | -----
200  | Esito positivo, viene rilevato un corpo della risposta.
201  | Esito positivo e la risorsa è stato creato.
202  | Esito positivo, la richiesta è stata accettata, ma alcune operazioni potrebbe essere ancora incomplete e completato in modo asincrono.
204  | Esito positivo, ma non esiste alcun corpo della risposta.
301  | Un reindirizzamento permanente.
302  | Un reindirizzamento temporaneo.
400  | I parametri nell'URL oppure nel corpo della richiesta non sono validi.
401  | Le credenziali fornite non sono validi.
403  | L'azione non è consentito specificato le credenziali fornite.
404  | La risorsa richiesta non esiste.
409  | La richiesta è in conflitto con una risorsa esistente.
500  | Il servizio ha rilevato un errore imprevisto.
503  | Il servizio è temporaneamente non disponibile.

Qualsiasi `GET` richiesta effettuata a un endpoint API può restituire un reindirizzamento HTTP (301 o 302). I client devono gestire correttamente questi reindirizzamenti osservando il `Location` intestazione e una successiva esecuzione `GET`. La documentazione relativa a endpoint specifici non esplicitamente chiamerà out in reindirizzamenti possono essere utilizzati.

Nel caso di un codice di stato di livello 500, il client può implementare un meccanismo di Riprova ragionevole. Gli ufficiale NuGet client tentativi tre volte in presenza di qualsiasi codice di stato di livello 500 o errore TCP/DNS.

## <a name="http-request-headers"></a>Intestazioni delle richieste HTTP

nome                     | Descrizione
------------------------ | -----------
X-NuGet-ApiKey           | Obbligatorio per push e l'eliminazione, vedere [ `PackagePublish` risorse](package-publish-resource.md)
X---versione del Client NuGet   | **Deprecato** e sostituito da`X-NuGet-Protocol-Version`
Versione protocollo di NuGet X | Obbligatorio in alcuni casi solo in nuget.org, vedere [nuget.org protocolli](NuGet-Protocols.md)

## <a name="authentication"></a>Autenticazione

L'autenticazione è lasciata l'implementazione per definire origine del pacchetto. Per nuget.org, solo il `PackagePublish` risorsa richiede l'autenticazione tramite un'intestazione di chiave API speciale. Vedere [ `PackagePublish` risorse](package-publish-resource.md) per informazioni dettagliate.
