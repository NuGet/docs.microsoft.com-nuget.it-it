---
title: API NuGet, repository firme | Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: La risorsa di firme del repository consente ai client di origini dei pacchetti di annunciare il repository di funzionalità di firma.
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 50f309b99d4bf59e14f3e29b6b0421d8c3e8aa5a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547981"
---
# <a name="repository-signatures"></a>Firme di repository

Se un'origine pacchetto supporta le firme di aggiunta repository per i pacchetti pubblicati, è possibile che un client di determinare i certificati di firma utilizzati per l'origine del pacchetto. Questa risorsa consente ai client di rilevare se un repository firmato pacchetto è stato manomesso o ha un certificato di firma imprevisto.

La risorsa usata per recuperare informazioni sulla firma questo repository è il `RepositorySignatures` trovare la risorsa nella [indice del servizio](service-index.md).

> [!Note]
> NuGet.org inizierà l'annuncio di `RepositorySignatures` risorse in un prossimo futuro.

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` valore viene usato:

Valore di @type                | Note
-------------------------- | -----
RepositorySignatures/4.7.0 | La versione iniziale

## <a name="base-url"></a>URL di base

URL del punto di ingresso per le API seguenti è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore. In questo argomento Usa l'URL segnaposto `{@id}`.

Si noti che a differenza di altre risorse, il `{@id}` l'URL è obbligatorio per essere serviti tramite HTTPS.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nei metodi di supporto solo HTTP di repository le firme resource `GET` e `HEAD`.

## <a name="repository-signatures-index"></a>Indice delle firme del repository

L'indice di firme di repository contiene due tipi di informazioni:

1. Se tutti i pacchetti disponibili nell'origine sono firmati da questa origine pacchetto repository.
1. L'elenco dei certificati usati per l'origine del pacchetto per firmare i pacchetti.

Nella maggior parte dei casi, l'elenco dei certificati verrà aggiunto sempre a. I nuovi certificati verranno aggiunto all'elenco quando il certificato di firma precedente è scaduto e l'origine del pacchetto deve iniziare a usare un nuovo certificato di firma. Se un certificato viene rimosso dall'elenco, che significa che tutte le firme dei pacchetti create con il certificato di firma rimosso non è più da considerare valide dal client. In questo caso, la firma del pacchetto, ma non necessariamente il pacchetto, non è valido. Un criterio client può consentire l'installazione del pacchetto come senza segno.

Nel caso di revoca del certificato (ad esempio, venga compromessa), l'origine del pacchetto deve firmare di nuovo tutti i pacchetti firmati dal certificato interessato. Inoltre, l'origine del pacchetto deve rimuovere il certificato interessato dall'elenco di certificati di firma.

La richiesta seguente recupera l'indice di firme di repository.

    GET {@id}

L'indice di firma del repository è un documento JSON che contiene un oggetto con le proprietà seguenti:

nome                | Tipo             | Obbligatorio
------------------- | ---------------- | --------
allRepositorySigned | boolean          | sì
signingCertificates | Matrice di oggetti | sì

Il `allRepositorySigned` valore booleano è impostato su false se l'origine del pacchetto ha alcuni pacchetti che non hanno alcuna firma dell'archivio. Se il valore booleano è impostato su true, tutti i pacchetti disponibili in origine deve avere una firma di repository prodotta da uno dei certificati di firma menzionati `signingCertificates`.

Deve essere presente uno o più certificati di firma nel `signingCertificates` matrice se il `allRepositorySigned` valore booleano è impostato su true. Se la matrice è vuota e `allRepositorySigned` è impostato su true, tutti i pacchetti dall'origine devono essere considerati validi, anche se un criterio client consentono ancora il consumo dei pacchetti. Ogni elemento nella matrice è un oggetto JSON con le proprietà seguenti.

nome         | Tipo   | Obbligatorio | Note
------------ | ------ | -------- | -----
contentUrl   | stringa | sì      | URL assoluto per il certificato pubblico con codifica DER
impronte digitali | object | sì      |
Oggetto      | stringa | sì      | Il nome distinto del soggetto del certificato
issuer       | stringa | sì      | Il nome distinto dell'emittente del certificato
notBefore    | stringa | sì      | Il timestamp di inizio del periodo di validità del certificato
notAfter     | stringa | sì      | Il timestamp finale del periodo di validità del certificato

Si noti che il `contentUrl` deve essere gestito tramite HTTPS. Questo URL non ha alcun modello di URL specifico e deve essere individuato in modo dinamico utilizzando questo documento di repository le firme dell'indice. 

Tutte le proprietà in questo oggetto (oltre `contentUrl`) deve essere derivabile dal certificato, vedere `contentUrl`.
Queste proprietà derivabile sono fornite per praticità per ridurre i round trip.

Il `fingerprints` oggetto presenta le proprietà seguenti:

nome                   | Tipo   | Obbligatorio | Note
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | stringa | sì      | L'impronta digitale SHA-256

Il nome della chiave `2.16.840.1.101.3.4.2.1` è l'OID dell'algoritmo hash SHA-256.

Tutti i valori hash devono essere rappresentazioni di stringa di caratteri minuscoli, con codifica esadecimale di digest hash.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
