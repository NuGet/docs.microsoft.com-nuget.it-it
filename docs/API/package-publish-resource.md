---
title: Push e Delete, NuGet API | Documenti Microsoft
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti e l'esclusione o eliminare i pacchetti esistenti.
keywords: Pacchetto NuGet API push API NuGet eliminare pacchetto, API NuGet esclusione di pacchetto, pacchetto di caricamento API NuGet, API NuGet creare pacchetto
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a>Push ed eliminare

È possibile eseguire il push, eliminare o esclusione, a seconda dell'implementazione di server e rimettere pacchetti utilizzando l'API di NuGet V3. Queste operazioni sono basate sul `PackagePublish` risorse, vedere il [indice servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Le operazioni seguenti `@type` valore viene utilizzato:

Valore di @type          | Note
-------------------- | -----
PackagePublish/2.0.0 | La versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore della `@id` proprietà del `PackagePublish/2.0.0` risorse nell'origine del pacchetto [indice servizio](service-index.md). Per la documentazione riportata di seguito, viene utilizzato l'URL di nuget.org. Prendere in considerazione `https://www.nuget.org/api/v2/package` come segnaposto per il `@id` valore trovato in corrispondenza dell'indice del servizio.

Si noti che questo URL punti nello stesso percorso dell'endpoint di push V2 legacy, poiché il protocollo è gli stessi.

## <a name="http-methods"></a>Metodi HTTP

Il `PUT`, `POST` e `DELETE` metodi HTTP supportati da questa risorsa. Per i metodi supportati per ogni endpoint, vedere di seguito.

## <a name="push-a-package"></a>Push di un pacchetto

> [!Note]
> ha NuGet.org [requisiti aggiuntivi](NuGet-Protocols.md) per l'interazione con l'endpoint di push.

NuGet.org supporta l'inserimento di nuovi pacchetti utilizzando l'API seguente. Se il pacchetto con la versione e l'ID specificato esiste già, nuget.org rifiuterà il push. Altre origini pacchetto supportino la sostituzione di un pacchetto esistente.

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

La chiave API è una stringa opaca disponibili dall'origine del pacchetto per l'utente e configurato nel client. Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare dimensioni per i valori dell'intestazione HTTP.

### <a name="request-body"></a>Corpo della richiesta

Il corpo della richiesta deve essere nel formato seguente:

#### <a name="multipart-form-data"></a>Dati del form multipart

L'intestazione della richiesta `Content-Type` è `multipart/form-data` e i byte non elaborati del .nupkg viene inserito il primo elemento nel corpo della richiesta. Gli elementi successivi in più parti corpo vengono ignorati. Il nome del file o qualsiasi altra intestazione degli elementi in più parti vengono ignorata.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
201, 202    | Il pacchetto è stato inserito correttamente
400         | Il pacchetto fornito non è valido
409         | Un pacchetto con la versione e l'ID specificato esiste già

Le implementazioni server variare il codice di stato di esito positivo restituito quando un pacchetto viene inserito correttamente.

## <a name="delete-a-package"></a>Eliminare un pacchetto

NuGet.org interpreta la richiesta di eliminazione del pacchetto come un'esclusione"di". Ciò significa che il pacchetto è ancora disponibile per i consumer esistenti del pacchetto, ma il pacchetto non viene più visualizzata nei risultati della ricerca o nell'interfaccia web. Per ulteriori informazioni su questa esercitazione, vedere il [pacchetti eliminati](../policies/deleting-packages.md) criteri. Altre implementazioni di server sono disponibili per interpretare il segnale come un'eliminazione di disco rigido, eliminare temporaneamente o esclusione. Ad esempio, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (un'implementazione di server supportano solo l'API V2 precedente) supporta la gestione di questa richiesta come un unlist o una disco rigida delete basata su un'opzione di configurazione.

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
Id             | URL    | stringa | sì      | L'ID del pacchetto da eliminare
VERSION        | URL    | stringa | sì      | La versione del pacchetto da eliminare
X-NuGet-ApiKey | Header | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
204         | Il pacchetto è stato eliminato
404         | Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste

## <a name="relist-a-package"></a>Rimettere un pacchetto

Se un pacchetto è incluso nell'elenco, è possibile rendere nuovamente visibili nei risultati della ricerca utilizzando l'endpoint "rimettere in vendita" che il pacchetto. Questo endpoint è la stessa forma di [eliminare (esclusione) endpoint](#delete-a-package) ma utilizza il `POST` metodo HTTP invece del `DELETE` metodo.

Se il pacchetto è già presente, viene comunque completato correttamente la richiesta.

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
Id             | URL    | stringa | sì      | L'ID del pacchetto rimettere in
VERSION        | URL    | stringa | sì      | La versione del pacchetto rimettere in
X-NuGet-ApiKey | Header | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
200         | Il pacchetto è ora elencato
404         | Nessun pacchetto con l'oggetto fornito `ID` e `VERSION` esiste
