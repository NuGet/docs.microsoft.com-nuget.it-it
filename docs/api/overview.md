---
title: Panoramica dell'API di NuGet
description: L'API NuGet è un set di endpoint HTTP che può essere utilizzato per scaricare i pacchetti, recuperare i metadati, pubblicare nuovi pacchetti e così via.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 770173d6b84048cf42a5da46cbc474d8cf604a08
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547503"
---
# <a name="nuget-api"></a>API NuGet

L'API NuGet è un set di endpoint HTTP che può essere utilizzato per scaricare i pacchetti, recuperare i metadati, pubblicare nuovi pacchetti e di eseguire la maggior parte delle altre operazioni disponibili nei client NuGet ufficiale.

Questa API viene usata dal client di NuGet in Visual Studio, nuget.exe e la CLI di .NET per eseguire operazioni di NuGet, ad esempio [ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore), ricerca nell'interfaccia utente di Visual Studio, e [ `nuget.exe push` ](../tools/cli-ref-push.md).

Si noti in alcuni casi, nuget.org prevede requisiti aggiuntivi che non vengono applicati da altre origini di pacchetti. Queste differenze sono documentate in base il [protocolli di nuget.org](nuget-protocols.md).

Per una semplice enumerazione e il download delle versioni nuget.exe disponibili, vedere la [tools.json](tools-json.md) endpoint.

## <a name="service-index"></a>Indice del servizio

Il punto di ingresso per l'API è un documento JSON in una posizione nota. Questo documento viene chiamato il **indice dei servizi**. Il percorso dell'indice del servizio per nuget.org è `https://api.nuget.org/v3/index.json`.

Questo documento JSON contiene un elenco di *risorse* che forniscono funzionalità diverse e soddisfare diversi casi d'uso.

I client che supportano l'API devono accettare uno o più di questi URL indice del servizio come metodo per la connessione alle origini del pacchetto corrispondente.

Per altre informazioni sull'indice di servizio, vedere [relativo riferimento all'API](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

L'API è versione 3 del protocollo HTTP di NuGet. Questo protocollo è talvolta detta "l'API di V3." Questi documenti di riferimento farà riferimento a questa versione del protocollo semplicemente come "l'API".

La versione dello schema di indice del servizio è indicata dal `version` proprietà nell'indice del servizio. L'API di utilizzo, è necessario che la stringa di versione abbia un numero di versione principale `3`. Quando vengono apportate modifiche non di rilievo allo schema di indice del servizio, versione secondaria della stringa di versione verrà aumentato.

I client meno recenti (ad esempio nuget.exe 2.x) non supportano l'API V3 e supportano solo l'API V2 precedenti, che non è illustrato qui.

API NuGet V3 è denominato in quanto tale perché è la nuova versione dell'API V2, di cui è stato il protocollo basato su OData implementato dalla versione 2.x del client NuGet ufficiale. L'API V3 inizialmente supportato dalla versione 3.0 del client NuGet ufficiale ed è ancora la versione più recente principali protocollo supportata dal client di NuGet, 4.0 e su. 

Delle modifiche ai protocolli non sostanziale è apportate all'API poiché era prima versione.

## <a name="resources-and-schema"></a>Risorse e dello schema

Il **indice dei servizi** descrive una serie di risorse. Il set corrente di risorse supportati sono i seguenti:

Nome della risorsa                                                          | Obbligatorio | Descrizione
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | sì      | Effettuare il push ed eliminare o rimuovere dall'elenco dei pacchetti.
[`SearchQueryService`](search-query-service-resource.md)               | sì      | Filtrare e cercare i pacchetti dalla parola chiave.
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | sì      | Ottenere i metadati del pacchetto.
[`PackageBaseAddress`](package-base-address-resource.md)               | sì      | Ottenere il contenuto del pacchetto (con estensione nupkg).
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | No       | Individuare gli ID di pacchetto e le versioni da sottostringa.
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | No       | Costruire un URL per accedere a una pagina web "per segnalare abusi".
[`RepositorySignatures`](repository-signatures-resource.md)            | No       | Ottenere i certificati usati per la firma del repository.
[`Catalog`](catalog-resource.md)                                       | No       | Record completo di tutti gli eventi del pacchetto.

In generale, tutti i dati non binari restituiti da una risorsa API vengono serializzati con JSON. Lo schema di risposta restituito da ogni risorsa nell'indice del servizio viene definito singolarmente per tale risorsa. Per altre informazioni sulle singole risorse, vedere gli argomenti elencati in precedenza.

> [!Note]
> Quando un'origine non implementa `SearchAutocompleteService` qualsiasi comportamento di completamento automatico deve essere disabilitata correttamente. Quando `ReportAbuseUriTemplate` non viene implementata, l'opta client NuGet ufficiale per di nuget.org segnalare abusi URL (rilevati dal [NuGet/Home & 4924](https://github.com/NuGet/Home/issues/4924)). Altri client può optare per un URL per segnalare abusi di semplicemente non mostrare all'utente.

## <a name="timestamps"></a>Timestamp

Tutti i timestamp restituiti dall'API vengono ora UTC o in caso contrario, vengono specificati utilizzando [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) rappresentazione. 

## <a name="http-methods"></a>Metodi HTTP

Verbo   | Usa
------ | -----------
GET    | Esegue un'operazione di sola lettura, in genere il recupero dei dati.
HEAD   | Recupera le intestazioni di risposta per il corrispondente `GET` richiesta.
PUT    | Crea una risorsa che non esiste oppure, se esiste, lo aggiorna. Alcune risorse potrebbero non supportare l'aggiornamento.
DELETE | Dall'elenco o elimina una risorsa.

## <a name="http-status-codes"></a>Codici di stato HTTP

Codice | Descrizione
---- | -----
200  | Caso di esito positivo ed è presente un corpo della risposta.
201  | Success e la risorsa è stato creato.
202  | Esito positivo, la richiesta è stata accettata, ma alcune operazioni possono risultare incomplete e completate in modo asincrono.
204  | Esito positivo, ma non esiste alcun corpo della risposta.
301  | Un reindirizzamento permanente.
302  | Un reindirizzamento temporaneo.
400  | I parametri nell'URL o nel corpo della richiesta non sono validi.
401  | Le credenziali specificate non sono validi.
403  | L'azione non è consentito specificato le credenziali fornite.
404  | La risorsa richiesta non esiste.
409  | La richiesta è in conflitto con una risorsa esistente.
500  | Il servizio ha rilevato un errore imprevisto.
503  | Il servizio è temporaneamente non disponibile.

Qualsiasi `GET` richiesta effettuata a un endpoint API può restituire un reindirizzamento HTTP (301 o 302). I client dovrebbero gestire correttamente questi reindirizzamenti osservando la `Location` intestazione ed emissione di una successiva `GET`. Documentazione relativa a endpoint specifici non chiama in modo esplicito orizzontale in cui possono essere utilizzati i reindirizzamenti.

Nel caso di un codice di stato di livello 500, il client può implementare un meccanismo di ripetizione dei tentativi ragionevole. Gli ufficiale NuGet client tentativi tre volte in presenza di qualsiasi codice di stato di livello 500 o errore DNS TCP.

## <a name="http-request-headers"></a>Intestazioni della richiesta HTTP

nome                     | Descrizione
------------------------ | -----------
X-NuGet-ApiKey           | Obbligatorio per i push e delete, vedere [ `PackagePublish` risorsa](package-publish-resource.md)
X-NuGet-Client-Version   | **Deprecato** e sostituito da `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | Obbligatorio in determinati casi solo in nuget.org, vedere [protocolli di nuget.org](NuGet-Protocols.md)
X-NuGet-Session-Id       | *Facoltativo*. NuGet client v4.7 + identificano le richieste HTTP che fanno parte della stessa sessione client NuGet. Per la `PackageReference` presenti operazioni di ripristino è un id di sessione, per altri scenari, ad esempio, completamento automatico e `packages.config` ripristino potrebbero esserci diverse diversi id di sessione a causa di un modo in cui viene eseguito il codice.

## <a name="authentication"></a>Autenticazione

L'autenticazione viene eseguita fino al livello l'implementazione di origine del pacchetto da definire. Per nuget.org, solo il `PackagePublish` risorsa richiede l'autenticazione mediante una speciale intestazione della chiave API. Visualizzare [ `PackagePublish` risorsa](package-publish-resource.md) per informazioni dettagliate.
