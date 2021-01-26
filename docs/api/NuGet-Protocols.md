---
title: Protocolli nuget.org
description: Protocolli nuget.org in evoluzione per interagire con i client NuGet.
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773971"
---
# <a name="nugetorg-protocols"></a>Protocolli di nuget.org

Per interagire con nuget.org, è necessario che i client seguano alcuni protocolli. Poiché questi protocolli continuano a evolversi, i client devono identificare la versione del protocollo che usano quando chiamano API nuget.org specifiche. Ciò consente a nuget.org di introdurre modifiche in modo non sostanziale per i client precedenti.

> [!Note]
> Le API documentate in questa pagina sono specifiche per nuget.org e non è previsto che altre implementazioni di server NuGet introducano queste API. 

Per informazioni sull'API NuGet implementata a livello generale nell'ecosistema NuGet, vedere [Panoramica dell'API](overview.md).

In questo argomento vengono elencati diversi protocolli come e quando sono disponibili.

## <a name="nuget-protocol-version-410"></a>Versione del protocollo NuGet 4.1.0

Il protocollo 4.1.0 specifica l'uso delle chiavi Verify-scope per interagire con i servizi diversi da nuget.org per convalidare un pacchetto con un account nuget.org. Si noti che il `4.1.0` numero di versione è una stringa opaca, ma che coincide con la prima versione del client NuGet ufficiale che supporta questo protocollo.

La convalida garantisce che le chiavi API create dall'utente vengano utilizzate solo con nuget.org e che la verifica o la convalida da parte di un servizio di terze parti venga gestita tramite le chiavi monouso Verify-scope. Queste chiavi Verify-scope possono essere usate per convalidare che il pacchetto appartenga a un determinato utente (account) in nuget.org.

### <a name="client-requirement"></a>Requisito client

È necessario che i client passino l'intestazione seguente quando eseguono chiamate API per eseguire il **push** dei pacchetti in NuGet.org:

```
X-NuGet-Protocol-Version: 4.1.0
```

Si noti che l' `X-NuGet-Client-Version` intestazione ha una semantica simile, ma è riservata a essere usata solo dal client NuGet ufficiale. I client di terze parti devono usare l' `X-NuGet-Protocol-Version` intestazione e il valore.

Il protocollo di **push** è descritto nella documentazione relativa alla [ `PackagePublish` risorsa](package-publish-resource.md).

Se un client interagisce con i servizi esterni e deve verificare se un pacchetto appartiene a un determinato utente (account), deve usare il protocollo seguente e usare le chiavi Verify-scope e non le chiavi API da nuget.org.

### <a name="api-to-request-a-verify-scope-key"></a>API per richiedere una chiave Verify-scope

Questa API viene usata per ottenere una chiave Verify-scope per un autore di nuget.org per convalidare un pacchetto di proprietà di loro.

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Type   | Necessario | Note
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | sì      | Identidier del pacchetto per il quale viene richiesta la chiave di ambito Verify
VERSION        | URL    | string | no       | Versione del pacchetto
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio: `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>Risposta

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API per verificare la chiave dell'ambito Verify

Questa API viene usata per convalidare una chiave Verify-scope per il pacchetto di proprietà dell'autore nuget.org.

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>Parametri della richiesta

Nome           | In     | Type   | Necessario | Note
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | sì      | Identificatore del pacchetto per il quale viene richiesta la chiave di ambito Verify
VERSION        | URL    | string | no       | Versione del pacchetto
X-NuGet-ApiKey | Intestazione | string | sì      | Ad esempio: `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> Questa chiave API dell'ambito di verifica scade entro un giorno o al primo utilizzo, a seconda di quale si verifica per primo.

#### <a name="response"></a>Risposta

Codice di stato | Significato
----------- | -------
200         | La chiave API è valida
403         | La chiave API non è valida o non è autorizzata a eseguire il push sul pacchetto
404         | Il pacchetto a cui `ID` fa riferimento e `VERSION` (facoltativo) non esiste
