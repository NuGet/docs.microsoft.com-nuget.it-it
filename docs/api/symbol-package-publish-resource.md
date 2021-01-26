---
title: Pacchetti di simboli push, API NuGet | Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Il servizio Publish consente ai client di pubblicare nuovi pacchetti di simboli.
keywords: Pacchetto di simboli push dell'API NuGet
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773891"
---
# <a name="push-symbol-packages"></a>Pacchetti di simboli push

È possibile eseguire il push dei pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando l'API NuGet V3.
Queste operazioni sono basate sulla `SymbolPackagePublish` risorsa presente nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

`@type`Viene utilizzato il valore seguente:

Valore della proprietà @type                 | Note
--------------------        | -----
SymbolPackagePublish/4.9.0  | Versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà della `SymbolPackagePublish/4.9.0` risorsa nell' [indice del servizio](service-index.md)dell'origine del pacchetto. Per la documentazione riportata di seguito, viene usato l'URL di NuGet. org. Considerare `https://www.nuget.org/api/v2/symbolpackage` come un segnaposto per il `@id` valore trovato nell'indice del servizio.

## <a name="http-methods"></a>Metodi HTTP

Il `PUT` metodo HTTP è supportato da questa risorsa. 

## <a name="push-a-symbol-package"></a>Eseguire il push di un pacchetto di simboli

nuget.org supporta il push del nuovo formato dei pacchetti di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) usando l'API seguente. 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

I pacchetti di simboli con lo stesso ID e la stessa versione possono essere inviati più volte. Un pacchetto di simboli verrà rifiutato nei casi seguenti.
- Non esiste un pacchetto con lo stesso ID e la stessa versione.
- È stato eseguito il push di un pacchetto di simboli con lo stesso ID e la stessa versione ma non è ancora pubblicato.
- Il pacchetto di simboli ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) non è valido (vedere [vincoli dei pacchetti di simboli](../create-packages/Symbol-Packages-snupkg.md)).

### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Type   | Necessario | Note
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`

La chiave API è una stringa opaca ottenuta dall'origine del pacchetto dall'utente e configurata nel client. Non è richiesto alcun formato stringa particolare, ma la lunghezza della chiave API non deve superare una dimensione ragionevole per i valori dell'intestazione HTTP.

### <a name="request-body"></a>Testo della richiesta

Il corpo della richiesta per il push dei simboli è uguale al corpo della richiesta di una richiesta di push del pacchetto (vedere [push e eliminazione di pacchetti](package-publish-resource.md)). 

### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
201         | Push del pacchetto di simboli completato.
400         | Il pacchetto di simboli specificato non è valido.
401         | L'utente non è autorizzato a eseguire questa azione.
404         | Non esiste un pacchetto corrispondente con l'ID e la versione specificati.
409         | È stato eseguito il push di un pacchetto di simboli con l'ID e la versione specificati, che tuttavia non è ancora disponibile.
413         | Il pacchetto è troppo grande.

