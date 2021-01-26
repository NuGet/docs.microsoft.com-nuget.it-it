---
title: Push ed eliminazione, API NuGet
description: Il servizio Publish consente ai client di pubblicare nuovi pacchetti ed eliminare dall'elenco o eliminare i pacchetti esistenti.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773919"
---
# <a name="push-and-delete"></a>Push ed eliminazione

È possibile eseguire il push, eliminare o rimuovere l'elenco in base all'implementazione del server e rielencare i pacchetti usando l'API NuGet V3. Queste operazioni sono basate sulla `PackagePublish` risorsa presente nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

`@type`Viene utilizzato il valore seguente:

Valore della proprietà @type          | Note
-------------------- | -----
PackagePublish/2.0.0 | Versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà della `PackagePublish/2.0.0` risorsa nell' [indice del servizio](service-index.md)dell'origine del pacchetto. Per la documentazione riportata di seguito, viene usato l'URL di NuGet. org. Considerare `https://www.nuget.org/api/v2/package` come un segnaposto per il `@id` valore trovato nell'indice del servizio.

Si noti che questo URL punta alla stessa posizione dell'endpoint di push V2 legacy poiché il protocollo è lo stesso.

## <a name="http-methods"></a>Metodi HTTP

I `PUT` `POST` metodi, e `DELETE` http sono supportati da questa risorsa. Per i metodi supportati in ogni endpoint, vedere di seguito.

## <a name="push-a-package"></a>Eseguire il push di un pacchetto

> [!Note]
> nuget.org presenta [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.

nuget.org supporta il push di nuovi pacchetti usando l'API seguente. Se il pacchetto con l'ID e la versione specificati esiste già, nuget.org rifiuterà il push. Altre origini di pacchetti possono supportare la sostituzione di un pacchetto esistente.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Type   | Necessario | Note
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`

La chiave API è una stringa opaca ottenuta dall'origine del pacchetto dall'utente e configurata nel client. Non è richiesto alcun formato stringa particolare, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori dell'intestazione HTTP.

### <a name="request-body"></a>Testo della richiesta

Il corpo della richiesta deve avere il formato seguente:

#### <a name="multipart-form-data"></a>Dati in formato multipart

L'intestazione della richiesta `Content-Type` è `multipart/form-data` e il primo elemento nel corpo della richiesta è costituito dai byte non elaborati del nupkg di cui viene eseguito il push. Gli elementi successivi nel corpo multipart vengono ignorati. Il nome del file o qualsiasi altra intestazione degli elementi multipart viene ignorato.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
201, 202    | Push del pacchetto completato
400         | Il pacchetto specificato non è valido
409         | Esiste già un pacchetto con l'ID e la versione specificati

Le implementazioni del server variano in base al codice di stato di esito positivo restituito quando viene eseguito il push di un pacchetto.

## <a name="delete-a-package"></a>Eliminare un pacchetto

nuget.org interpreta la richiesta di eliminazione del pacchetto come "Unlist". Questo significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzato nei risultati della ricerca o nell'interfaccia Web. Per ulteriori informazioni su questa procedura, vedere i criteri dei [pacchetti eliminati](../nuget-org/policies/deleting-packages.md) . Altre implementazioni del server sono gratuite per interpretare questo segnale come eliminazione, eliminazione temporanea o annullamento dell'elenco. Ad esempio, [NuGet. Server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione del server che supporta solo la versione precedente dell'API v2) supporta la gestione della richiesta come Unlist o DELETE rigido in base a un'opzione di configurazione.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Type   | Necessario | Note
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | sì      | ID del pacchetto da eliminare
VERSION        | URL    | string | sì      | Versione del pacchetto da eliminare
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
204         | Il pacchetto è stato eliminato
404         | Nessun pacchetto con l'oggetto fornito `ID` ed `VERSION` esiste

## <a name="relist-a-package"></a>Rielencare un pacchetto

Se un pacchetto non è incluso nell'elenco, è possibile renderlo ancora una volta visibile nei risultati della ricerca usando l'endpoint "relist". Questo endpoint ha la stessa forma dell' [endpoint Delete (Unlist)](#delete-a-package) , ma usa il `POST` metodo HTTP anziché il `DELETE` metodo.

Se il pacchetto è già elencato, la richiesta ha ancora esito positivo.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Type   | Necessario | Note
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | sì      | ID del pacchetto da rielencare
VERSION        | URL    | string | sì      | Versione del pacchetto da rielencare
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
200         | Il pacchetto è ora elencato
404         | Nessun pacchetto con l'oggetto fornito `ID` ed `VERSION` esiste
