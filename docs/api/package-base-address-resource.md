---
title: Contenuto del pacchetto, NuGet API
description: L'indirizzo di base del pacchetto è una semplice interfaccia per recuperare il pacchetto stesso.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547154"
---
# <a name="package-content"></a>Contenuto del pacchetto

È possibile generare un URL per recuperare il contenuto del pacchetto arbitrario (file nupkg) usando l'API di V3. La risorsa usata per recuperare il contenuto del pacchetto è il `PackageBaseAddress` trovare la risorsa nella [indice del servizio](service-index.md). Questa risorsa consente anche l'individuazione di tutte le versioni di un pacchetto, elencati o non in elenco.

Questa risorsa è noto come entrambi il "pacchetto base address" o il contenitore"flat".

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` valore viene usato:

Valore di @type              | Note
------------------------ | -----
PackageBaseAddress/3.0.0 | La versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore della `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL disponibili il supporto di risorse di registrazione i metodi HTTP `GET` e `HEAD`.

## <a name="enumerate-package-versions"></a>Enumera le versioni dei pacchetti

Se il client riconosce un ID pacchetto e vuole scoprire quali versioni dei pacchetti il pacchetto di origine è disponibile, il client può costruire un URL prevedibile per enumerare tutte le versioni del pacchetto. Questo elenco deve essere un "elenco di directory" per l'API di pacchetto contenuto indicato di seguito.

> [!Note]
> Questo elenco contiene entrambe le versioni dei pacchetti elencati e non in elenco.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametri della richiesta

nome     | In     | Tipo    | Obbligatorio | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | stringa  | sì      | L'ID del pacchetto, lettere minuscole

Il `LOWER_ID` valore è l'ID pacchetto desiderato minuscola usando le regole implementate da. Di NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (metodo).

### <a name="response"></a>Risposta

Se l'origine del pacchetto non ci è versioni dell'ID del pacchetto fornito, viene restituito un codice di 404 stato.

Se l'origine del pacchetto ha una o più versioni, viene restituito un codice di 200 stato. Il corpo della risposta è un oggetto JSON con la proprietà seguente:

nome     | Tipo             | Obbligatorio | Note
-------- | ---------------- | -------- | -----
versioni | Matrice di stringhe | sì      | L'ID pacchetto

Le stringhe nel `versions` matrice tutte minuscole, [normalizzato le stringhe di versione di NuGet](../reference/package-versioning.md#normalized-version-numbers). Le stringhe di versione non contengono i metadati di compilazione di SemVer 2.0.0.

L'intento è che le stringhe di versione disponibili in questa matrice possono essere usate come verbatim per il `LOWER_VERSION` token trovato nell'endpoint seguenti.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Scarica contenuto pacchetto (con estensione nupkg)

Se il client sa un ID pacchetto e versione e si vuole scaricare il contenuto del pacchetto, è sufficiente creare l'URL seguente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametri della richiesta

nome          | In     | Tipo   | Obbligatorio | Note
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | stringa | sì      | L'ID del pacchetto, lettere minuscole
LOWER_VERSION | URL    | stringa | sì      | La versione del pacchetto, normalizzate e minuscola

Entrambe `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Di NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
ProcessOnStatus.

Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata mediante una versione di NuGet [regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers). Ciò significa che i metadati di compilazione che sono consentito dalla specifica di SemVer 2.0.0 devono essere escluse in questo caso.

### <a name="response-body"></a>Corpo della risposta

Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato. Il corpo della risposta sarà contenuto il pacchetto stesso.

Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Risposta di esempio

Il flusso di dati binari è il pacchetto. nupkg per newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Scaricare il manifesto di pacchetto (con estensione nuspec)

Se il client sa un ID pacchetto e versione e si vuole scaricare il manifesto del pacchetto, è sufficiente creare l'URL seguente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametri della richiesta

nome          | In     | Tipo    | Obbligatorio | Note
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | stringa  | sì      | L'ID del pacchetto, lettere minuscole
LOWER_VERSION | URL    | numero intero | sì      | La versione del pacchetto, normalizzate e minuscola

Entrambe `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Di NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) (metodo).

Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata mediante una versione di NuGet [regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers). Ciò significa che i metadati di compilazione che sono consentito dalla specifica di SemVer 2.0.0 devono essere escluse in questo caso.

### <a name="response-body"></a>Corpo della risposta

Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato. Il corpo della risposta sarà il manifesto di pacchetto, ovvero il file con estensione nuspec contenuti nel pacchetto. nupkg corrispondente. Il file con estensione nuspec è un documento XML.

Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Risposta di esempio

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
