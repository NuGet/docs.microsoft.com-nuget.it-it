---
title: Push ed eliminazione, API NuGet
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti e rimuovere dall'elenco o Elimina i pacchetti esistenti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426718"
---
# <a name="push-and-delete"></a>Push ed eliminazione

È possibile eseguire il push, eliminare o rimuovere dall'elenco, a seconda dell'implementazione di server e includere di nuovo nell'elenco dei pacchetti tramite l'API di NuGet V3. Queste operazioni si basano all'esterno della `PackagePublish` trovare la risorsa nella [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` valore viene usato:

Valore di@type          | Note
-------------------- | -----
PackagePublish/2.0.0 | La versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore della `@id` proprietà del `PackagePublish/2.0.0` risorsa nell'origine del pacchetto [indice del servizio](service-index.md). Per la documentazione seguente, viene usato l'URL di nuget.org. Prendere in considerazione `https://www.nuget.org/api/v2/package` come segnaposto per il `@id` valore trovato nell'indice del servizio.

Si noti che questo URL punta a nello stesso percorso degli endpoint precedenti V2 push, poiché il protocollo è gli stessi.

## <a name="http-methods"></a>Metodi HTTP

Il `PUT`, `POST` e `DELETE` metodi HTTP supportati da questa risorsa. Per i metodi che sono supportati in ogni endpoint, vedere di seguito.

## <a name="push-a-package"></a>Push di un pacchetto

> [!Note]
> dispone di NuGet.org [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.

NuGet.org supporta il push dei nuovi pacchetti tramite l'API seguente. Se il pacchetto con l'ID e versione specificati esiste già, nuget.org rifiuterà il push. Altre origini di pacchetti possono supportare la sostituzione di un pacchetto esistente.

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

La chiave API è una stringa opaca ricevuto dall'origine del pacchetto dall'utente e configurato nel client. Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori delle intestazioni HTTP.

### <a name="request-body"></a>Corpo della richiesta

Il corpo della richiesta deve essere nel formato seguente:

#### <a name="multipart-form-data"></a>Dati del form multipart

L'intestazione della richiesta `Content-Type` è `multipart/form-data` e il primo elemento nel corpo della richiesta è i byte non elaborati del pacchetto. nupkg esserne eseguito il push. Gli elementi successivi in più parti corpo vengono ignorati. Il nome del file o qualsiasi altra intestazione degli elementi composti da più parti verranno ignorata.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
201, 202    | Il pacchetto è stato eseguito il push
400         | Il pacchetto fornito non è valido
409         | Un pacchetto con l'ID e versione specificati esiste già

Le implementazioni di server variano il codice di stato riuscito restituito quando un pacchetto viene eseguito il push.

## <a name="delete-a-package"></a>Eliminare un pacchetto

NuGet.org interpreta la richiesta di eliminazione del pacchetto come un' "Rimuovi dall'elenco". Ciò significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzata nei risultati della ricerca o nell'interfaccia web. Per altre informazioni su questa procedura, vedere la [i pacchetti eliminati](../nuget-org/policies/deleting-packages.md) criteri. Altre implementazioni di server sono liberi di interpretare questo segnale come un'eliminazione di disco rigido, tipo "soft" eliminare o rimuovere dall'elenco. Ad esempio, [NuGet. server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione del server che supportano solo l'API V2 meno recente) supporta la gestione di questa richiesta come una rimozione dall'elenco o una disco rigida delete basata su un'opzione di configurazione.

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
Id             | URL    | string | sì      | L'ID del pacchetto da eliminare
VERSION        | URL    | string | sì      | La versione del pacchetto da eliminare
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
204         | Il pacchetto è stato eliminato
404         | Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste

## <a name="relist-a-package"></a>Includere di nuovo nell'elenco un pacchetto

Se un pacchetto è incluso nell'elenco, è possibile rendere nuovamente visibile nei risultati della ricerca usando l'endpoint "rimessa" che il pacchetto. Questo endpoint è la stessa forma il [eliminare (rimuovere dall'elenco) endpoint](#delete-a-package) , ma usa le `POST` invece del metodo HTTP il `DELETE` (metodo).

Se il pacchetto è già presente, viene comunque completato correttamente la richiesta.

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
Id             | URL    | string | sì      | L'ID del pacchetto rimettere in
VERSION        | URL    | string | sì      | La versione del pacchetto rimettere in
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
200         | Il pacchetto è ora elencato
404         | Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste
