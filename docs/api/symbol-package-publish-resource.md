---
title: Eseguire il push dei pacchetti di simboli, API NuGet | Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Il servizio di pubblicazione consente ai client di pubblicare nuovi pacchetti di simboli.
keywords: Pacchetto di simboli di API NuGet push
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580414"
---
# <a name="push-symbol-packages"></a>Eseguire il push dei pacchetti di simboli

È possibile push dei pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) tramite l'API di NuGet V3.
Queste operazioni si basano all'esterno della `SymbolPackagePublish` trovare la risorsa nella [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` valore viene usato:

Valore di @type                 | Note
--------------------        | -----
SymbolPackagePublish/4.9.0  | La versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore della `@id` proprietà del `SymbolPackagePublish/4.9.0` risorsa nell'origine del pacchetto [indice del servizio](service-index.md). Per la documentazione seguente, viene usato l'URL di nuget.org. Prendere in considerazione `https://www.nuget.org/api/v2/symbolpackage` come segnaposto per il `@id` valore trovato nell'indice del servizio.

## <a name="http-methods"></a>Metodi HTTP

Il `PUT` metodo HTTP supportato da questa risorsa. 

## <a name="push-a-symbol-package"></a>Push di un pacchetto di simboli

NuGet.org supporta il push dei nuovo formato di pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando l'API seguente. 

    PUT https://www.nuget.org/api/v2/symbolpackage

Pacchetti di simboli con lo stesso ID e versione possono essere inviati più volte. Un pacchetto di simboli verrà rifiutato nei casi seguenti.
- Un pacchetto con lo stesso ID e versione non esiste.
- Un pacchetto di simboli con lo stesso ID e versione è stato eseguito il push, ma non ancora pubblicato.
- Il pacchetto di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) non è valido (vedere [vincoli di pacchetto di simboli](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Intestazione | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

La chiave API è una stringa opaca ricevuto dall'origine del pacchetto dall'utente e configurato nel client. Nessun formato determinata stringa è obbligatoria, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori delle intestazioni HTTP.

### <a name="request-body"></a>Corpo della richiesta

Il corpo della richiesta per il push di simbolo è uguale a quello con il corpo della richiesta di una richiesta di push del pacchetto (vedere [push del pacchetto ed eliminare](package-publish-resource.md)). 

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
201         | Il pacchetto di simboli è stato eseguito il push.
400         | Il pacchetto di simboli specificato non è valido.
401         | L'utente non è autorizzato a eseguire questa azione.
404         | Un pacchetto corrispondente con l'ID e la versione specificata non esiste.
409         | È stato eseguito il push di un pacchetto di simboli con l'ID e versione specificati, ma non è ancora disponibile.
413         | Il pacchetto è troppo grande.

