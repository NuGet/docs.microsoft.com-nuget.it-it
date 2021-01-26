---
title: Firme del repository, API NuGet | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La risorsa firme del repository consente alle origini dei pacchetti client di annunciare le funzionalità di firma del repository.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775338"
---
# <a name="repository-signatures"></a>Firme di repository

Se un'origine del pacchetto supporta l'aggiunta di firme di repository ai pacchetti pubblicati, è possibile che un client determini i certificati di firma utilizzati dall'origine del pacchetto. Questa risorsa consente ai client di rilevare se un pacchetto firmato del repository è stato alterato o ha un certificato di firma imprevisto.

La risorsa usata per recuperare le informazioni sulla firma del repository è la `RepositorySignatures` risorsa trovata nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

`@type`Viene utilizzato il valore seguente:

Valore della proprietà @type                | Note
-------------------------- | -----
RepositorySignatures/4.7.0 | Versione iniziale
RepositorySignatures/4.9.0 | Supportato da NuGet v 4.9 + client
RepositorySignatures/5.0.0 | Consente l'abilitazione di `allRepositorySigned` . Supportato da NuGet v 5.0 + client

## <a name="base-url"></a>URL di base

L'URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associata al valore di risorsa sopra menzionato `@type` . In questo argomento viene utilizzato l'URL segnaposto `{@id}` .

Si noti che, a differenza di altre risorse, `{@id}` è necessario che l'URL venga servito tramite HTTPS.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL presenti nella risorsa delle firme del repository supportano solo i metodi HTTP `GET` e `HEAD` .

## <a name="repository-signatures-index"></a>Indice delle firme del repository

L'indice delle firme del repository contiene due tipi di informazioni:

1. Indica se tutti i pacchetti trovati nell'origine sono repository firmati da questa origine del pacchetto.
1. Elenco di certificati utilizzati dall'origine del pacchetto per la firma dei pacchetti.

Nella maggior parte dei casi, l'elenco dei certificati verrà aggiunto solo a. I nuovi certificati vengono aggiunti all'elenco quando il certificato di firma precedente è scaduto e l'origine del pacchetto deve iniziare a usare un nuovo certificato di firma. Se un certificato viene rimosso dall'elenco, significa che tutte le firme dei pacchetti create con il certificato di firma rimosso non devono più essere considerate valide dal client. In questo caso, la firma del pacchetto, ma non necessariamente il pacchetto, non è valida. Un criterio client può consentire l'installazione del pacchetto come senza segno.

Nel caso di revoca del certificato (ad esempio, compromissione della chiave), è previsto che l'origine del pacchetto firmi nuovamente tutti i pacchetti firmati dal certificato interessato. Inoltre, l'origine del pacchetto deve rimuovere il certificato interessato dall'elenco dei certificati di firma.

La richiesta seguente recupera l'indice delle firme del repository.

```
GET {@id}
```

L'indice della firma del repository è un documento JSON che contiene un oggetto con le proprietà seguenti:

Nome                | Type             | Necessario | Note
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | sì      | Deve trovarsi `false` sulle risorse 4.7.0 e 4.9.0
signingCertificates | matrice di oggetti | sì      | 

Il `allRepositorySigned` valore booleano è impostato su false se l'origine del pacchetto include alcuni pacchetti senza firma del repository. Se il valore booleano è impostato su true, tutti i pacchetti disponibili nell'origine devono disporre di una firma del repository prodotta da uno dei certificati di firma indicati in `signingCertificates` .

> [!Warning]
> Il `allRepositorySigned` valore booleano deve essere false nelle risorse 4.7.0 e 4.9.0. I client NuGet v 4.7, v 4.8 e v 4.9 non possono installare pacchetti da origini che hanno `allRepositorySigned` impostato su true.

`signingCertificates`Se il `allRepositorySigned` valore booleano è impostato su true, nella matrice devono essere presenti uno o più certificati di firma. Se la matrice è vuota e `allRepositorySigned` è impostata su true, tutti i pacchetti dell'origine devono essere considerati non validi, sebbene i criteri client possano comunque consentire l'utilizzo di pacchetti. Ogni elemento in questa matrice è un oggetto JSON con le proprietà seguenti.

Nome         | Type   | Necessario | Note
------------ | ------ | -------- | -----
contentUrl   | string | sì      | URL assoluto del certificato pubblico con codifica DER
impronte digitali | object | sì      |
subject      | string | sì      | Nome distinto del soggetto del certificato
autorità di certificazione       | string | sì      | Nome distinto dell'emittente del certificato.
notBefore    | string | sì      | Timestamp iniziale del periodo di validità del certificato
notAfter     | string | sì      | Timestamp finale del periodo di validità del certificato

Si noti che `contentUrl` è necessario che sia servito tramite HTTPS. Questo URL non ha un modello di URL specifico e deve essere individuato in modo dinamico usando questo documento di indice delle firme del repository. 

Tutte le proprietà di questo oggetto (a parte `contentUrl` ) devono essere derivabili dal certificato trovato in `contentUrl` .
Queste proprietà derivabili vengono fornite come praticità per ridurre al minimo i round trip.

Di seguito sono elencate le proprietà dell'oggetto `fingerprints`:

Nome                   | Type   | Necessario | Note
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | sì      | Impronta digitale SHA-256

Il nome della chiave `2.16.840.1.101.3.4.2.1` è l'OID dell'algoritmo hash SHA-256.

Tutti i valori hash devono essere rappresentazioni di stringa con codifica esadecimale minuscole del digest hash.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
