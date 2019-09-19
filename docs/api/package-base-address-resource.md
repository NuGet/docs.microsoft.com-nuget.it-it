---
title: Contenuto del pacchetto, API NuGet
description: L'indirizzo di base del pacchetto è una semplice interfaccia per il recupero del pacchetto stesso.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094115"
---
# <a name="package-content"></a>Contenuto del pacchetto

È possibile generare un URL per recuperare il contenuto di un pacchetto arbitrario (il file con estensione nupkg) usando l'API V3. La risorsa utilizzata per il recupero del contenuto del pacchetto `PackageBaseAddress` è la risorsa presente nell' [indice del servizio](service-index.md). Questa risorsa consente inoltre l'individuazione di tutte le versioni di un pacchetto, elencate o riportate in elenco.

Questa risorsa viene comunemente definita "indirizzo di base del pacchetto" o come "contenitore Flat".

## <a name="versioning"></a>Controllo delle versioni

Viene utilizzato `@type` il valore seguente:

Valore di @type              | Note
------------------------ | -----
PackageBaseAddress/3.0.0 | Versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguenti è il valore della `@id` proprietà associata al valore di risorsa `@type` sopra menzionato. Nel documento seguente verrà usato l'URL `{@id}` di base segnaposto.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati nella risorsa di registrazione supportano i metodi `GET` http `HEAD`e.

## <a name="enumerate-package-versions"></a>Enumera versioni pacchetto

Se il client conosce un ID pacchetto e desidera individuare le versioni del pacchetto disponibili nell'origine del pacchetto, il client può costruire un URL stimabile per enumerare tutte le versioni dei pacchetti. Questo elenco è destinato a essere un "elenco di directory" per l'API del contenuto del pacchetto indicata di seguito.

> [!Note]
> Questo elenco contiene le versioni di pacchetto elencate e non in elenco.

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>Parametri della richiesta

Name     | In     | Type    | Obbligatoria | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | sì      | ID del pacchetto, minuscolo

Il `LOWER_ID` valore è l'ID pacchetto desiderato in minuscolo usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.

### <a name="response"></a>Risposta

Se l'origine del pacchetto non dispone di versioni dell'ID pacchetto fornito, viene restituito un codice di stato 404.

Se l'origine del pacchetto contiene una o più versioni, viene restituito un codice di stato 200. Il corpo della risposta è un oggetto JSON con la proprietà seguente:

Name     | Type             | Obbligatoria | Note
-------- | ---------------- | -------- | -----
versioni | Matrice di stringhe | sì      | Versioni disponibili

Le stringhe nella `versions` matrice sono tutte stringhe di versione di [NuGet normalizzate e normalizzate](../concepts/package-versioning.md#normalized-version-numbers). Le stringhe di versione non contengono metadati di compilazione SemVer 2.0.0.

Lo scopo è che le stringhe di versione trovate in questa matrice possano essere usate Verbatim per `LOWER_VERSION` i token trovati negli endpoint seguenti.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Scaricare il contenuto del pacchetto (. nupkg)

Se il client conosce un ID e una versione del pacchetto e vuole scaricare il contenuto del pacchetto, è sufficiente costruire l'URL seguente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>Parametri della richiesta

NOME          | In     | Type   | Obbligatoria | Note
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | sì      | ID del pacchetto, minuscolo
LOWER_VERSION | URL    | string | sì      | Versione del pacchetto, normalizzata e minuscola

Sia `LOWER_ID` che`LOWER_VERSION` sono minuscole usando le regole implementate da. NET[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
ProcessOnStatus.

È la versione del pacchetto desiderata normalizzata usando [le regole di normalizzazione](../concepts/package-versioning.md#normalized-version-numbers)della versione di NuGet. `LOWER_VERSION` Ciò significa che in questo caso i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere esclusi.

### <a name="response-body"></a>Corpo della risposta

Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di stato 200. Il corpo della risposta sarà il contenuto del pacchetto stesso.

Se il pacchetto non esiste nell'origine del pacchetto, viene restituito un codice di stato 404.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>Risposta di esempio

Flusso binario che rappresenta il file con estensione nupkg per Newtonsoft. JSON 9.0.1.

## <a name="download-package-manifest-nuspec"></a>Scarica il manifesto del pacchetto (. NuSpec)

Se il client conosce un ID e una versione del pacchetto e vuole scaricare il manifesto del pacchetto, è sufficiente costruire l'URL seguente:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>Parametri della richiesta

NOME          | In     | Type   | Obbligatoria | Note
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | sì      | ID del pacchetto, minuscolo
LOWER_VERSION | URL    | string | sì      | Versione del pacchetto, normalizzata e minuscola

Sia `LOWER_ID` che`LOWER_VERSION` sono minuscole usando le regole implementate da. [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) Metodo NET.

È la versione del pacchetto desiderata normalizzata usando [le regole di normalizzazione](../concepts/package-versioning.md#normalized-version-numbers)della versione di NuGet. `LOWER_VERSION` Ciò significa che in questo caso i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere esclusi.

### <a name="response-body"></a>Corpo della risposta

Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di stato 200. Il corpo della risposta sarà il manifesto del pacchetto, ovvero il file con estensione NuSpec contenuto nel file. nupkg corrispondente. Il file con estensione NuSpec è un documento XML.

Se il pacchetto non esiste nell'origine del pacchetto, viene restituito un codice di stato 404.

### <a name="sample-request"></a>Richiesta di esempio

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>Risposta di esempio

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
