---
title: Protocolli di NuGet.org
description: I protocolli di nuget.org in continua evoluzione per interagire con i client NuGet.
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822578"
---
# <a name="nugetorg-protocols"></a>protocolli di NuGet.org

Per interagire con nuget.org, è necessario seguire alcuni protocolli client. Poiché questi protocolli mantengono in evoluzione, i client devono identificare la versione del protocollo che usano durante la chiamata API di nuget.org specifico. In questo modo nuget.org introdurre modifiche in modo non è importante per i client precedenti.

> [!Note]
> Le API illustrate in questa pagina sono specifiche di nuget.org e vi è alcuna aspettativa per altre implementazioni di server NuGet introdurre tali API. 

Per informazioni sull'API NuGet implementato su vasta scala nell'ecosistema NuGet, vedere il [panoramica dell'API](overview.md).

Questo argomento elenca i vari protocolli come e quando si collegano a esistenza.

## <a name="nuget-protocol-version-410"></a>Versione del protocollo NuGet 4.1.0

Il 4.1.0 protocollo specifica l'utilizzo di chiavi di ambito verificare per interagire con i servizi diversi da nuget.org, per convalidare un pacchetto con un account di nuget.org. Si noti che il `4.1.0` versione numero è una stringa opaca, ma si verifica in genere coincidano con la prima versione del client NuGet ufficiale che questo protocollo è supportato.

La convalida garantisce che le chiavi API creati dall'utente vengono utilizzate solo con nuget.org e che altri verifica o convalida da un servizio di terze parti viene gestita tramite una chiave di ambito verificare usato una sola volta. Queste chiavi ambito verificare utilizzabile per convalidare che il pacchetto appartiene a un determinato utente (account) in nuget.org.

### <a name="client-requirement"></a>Requisiti client

I client devono passare l'intestazione seguente quando si effettuano chiamate API per **push** pacchetti nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Si noti che il `X-NuGet-Client-Version` intestazione semantica è simile, ma è riservato a essere utilizzato solo dal client NuGet ufficiale. I client di terze parti devono utilizzare il `X-NuGet-Protocol-Version` intestazione e il valore.

Il **push** protocollo stesso è descritto nella documentazione per il [ `PackagePublish` risorse](package-publish-resource.md).

Se un client interagisce con servizi esterni è necessario per convalidare un pacchetto appartiene a un determinato utente (account), deve utilizzare il protocollo seguente ed utilizzare le chiavi di verifica all'ambito e non le chiavi API di nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API per richiedere una chiave di verifica dell'ambito

Questa API viene usata per ottenere una chiave di verifica con ambito di un autore di nuget.org convalidare un pacchetto di proprietà di quest'ultimo.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
Id             | URL    | stringa | sì      | Identidier il pacchetto per il quale viene richiesta la chiave di verifica ambito
VERSION        | URL    | stringa | No       | La versione del pacchetto
X-NuGet-ApiKey | Header | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {USER_API_KEY}`.

#### <a name="response"></a>Risposta

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API per verificare la chiave di verifica ambito

Questa API viene usata per convalidare una chiave di verifica ambito per il pacchetto dall'autore del nuget.org di proprietà.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------  | ------ | ------ | -------- | -----
Id             | URL    | stringa | sì      | L'identificatore del pacchetto per il quale viene richiesta la chiave di verifica ambito
VERSION        | URL    | stringa | No       | La versione del pacchetto
X-NuGet-ApiKey | Header | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Questa chiave API ambito verifica scadenza ora del giorno o al primo utilizzo, qualunque si verifichi prima.

#### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
200         | La chiave API è valida
403         | La chiave API non è valido o non autorizzato per effettuare il push per il pacchetto
404         | Il pacchetto a cui fa riferimento a `ID` e `VERSION` (facoltativo) non esiste
