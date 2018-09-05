---
title: Protocolli di NuGet.org
description: I protocolli di nuget.org in continua evoluzione per interagire con i client NuGet.
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547273"
---
# <a name="nugetorg-protocols"></a>protocolli di NuGet.org

Per interagire con nuget.org, è necessario seguire alcuni protocolli client. Perché mantengano in continua evoluzione di questi protocolli, i client devono identificare la versione del protocollo che usano quando si chiamano le API di nuget.org specifico. In questo modo nuget.org per introdurre le modifiche in modo non di rilievo per i client precedenti.

> [!Note]
> Le API illustrate in questa pagina sono specifiche di nuget.org e vi è alcuna aspettativa per altre implementazioni di server NuGet per introdurre queste API. 

Per informazioni sull'API NuGet implementato su vasta scala nell'ecosistema NuGet, vedere la [panoramica dell'API](overview.md).

Questo argomento elenca i vari protocolli come e quando diventano di esistenza.

## <a name="nuget-protocol-version-410"></a>Versione del protocollo NuGet 4.1.0

La 4.1.0 protocollo specifica dell'utilizzo delle chiavi di verifica dell'ambito per interagire con servizi diversi da nuget.org, per convalidare un pacchetto in un account di nuget.org. Si noti che il `4.1.0` versione numero è una stringa opaca ma coincide con la prima versione del client NuGet ufficiale che questo protocollo è supportato.

La convalida garantisce che le chiavi API create dall'utente vengono utilizzate solo con nuget.org e che altri verifica o convalida da un servizio di terze parti viene gestita tramite una chiave di ambito verificare usato una sola volta. Queste chiavi verificare ambito sono utilizzabile per verificare che il pacchetto appartiene a un determinato utente (account) in nuget.org.

### <a name="client-requirement"></a>Requisiti del client

I client devono passare l'intestazione seguente quando si effettuano chiamate all'API **push** pacchetti da nuget.org:

    X-NuGet-Protocol-Version: 4.1.0

Si noti che il `X-NuGet-Client-Version` intestazione ha una semantica simile ma è riservata per essere utilizzato solo dai client NuGet ufficiale. I client di terze parti devono usare il `X-NuGet-Protocol-Version` intestazione e il valore.

Il **push** protocollo stesso è descritto nella documentazione per il [ `PackagePublish` risorsa](package-publish-resource.md).

Se un client interagisce con servizi esterni e deve verificare se un pacchetto a cui appartiene un determinato utente (account), dovrebbe usare il protocollo seguente e usare le chiavi di verifica-ambito e non le chiavi API da nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>Per richiedere una chiave di verifica dell'ambito dell'API

Questa API viene usata per ottenere una chiave di verifica dall'ambito di un autore di nuget.org convalidare un pacchetto di proprietà di quest'ultimo.

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------- | ------ | ------ | -------- | -----
Id             | URL    | stringa | sì      | Identidier il pacchetto per il quale viene richiesta la chiave di ambito di verifica
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

Questa API viene usata per convalidare una chiave di verifica dell'ambito per il pacchetto di proprietà dell'autore di nuget.org.

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>Parametri della richiesta

nome           | In     | Tipo   | Obbligatorio | Note
-------------  | ------ | ------ | -------- | -----
Id             | URL    | stringa | sì      | L'identificatore del pacchetto per il quale viene richiesta la chiave di ambito di verifica
VERSION        | URL    | stringa | No       | La versione del pacchetto
X-NuGet-ApiKey | Header | stringa | sì      | Ad esempio, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`.

> [!Note]
> Questo tasto di ambito API verifica scade tra ora del giorno o al primo utilizzo, a seconda di quale si verifica per primo.

#### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
200         | La chiave API è valida
403         | La chiave API non è valido o non autorizzato a eseguire il push per il pacchetto
404         | Il pacchetto a cui fa riferimento `ID` e `VERSION` (facoltativo) non esiste
