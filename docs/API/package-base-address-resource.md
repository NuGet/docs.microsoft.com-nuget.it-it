---
title: Pacchetto di contenuto, NuGet API | Documenti Microsoft
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
ms.assetid: ec68b5d1-a684-4995-b1a6-6210dbb24875
description: "L'indirizzo di base del pacchetto è un'interfaccia semplice per recuperare il pacchetto stesso."
keywords: NuGet flat contenitore, l'indirizzo di base del pacchetto NuGet, NuGet nupkg API, versioni del pacchetto NuGet API, API NuGet pacchetti non in elenco, API NuGet download nuspec
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: a581f9854410bc1a84d65310b38928a1d889ece2
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/05/2018
---
# <a name="package-content"></a>Contenuto del pacchetto

È possibile generare un URL per recuperare il contenuto del pacchetto non autorizzato (il file .nupkg) tramite l'API V3. La risorsa utilizzata per il recupero di contenuto del pacchetto è il `PackageBaseAddress` risorse, vedere il [indice servizio](service-index.md). Questa risorsa consente inoltre l'individuazione di tutte le versioni di un pacchetto, elencato o non in elenco.

Questa risorsa è noto come un "pacchetto indirizzo di base" o "container flat".

## <a name="versioning"></a>Controllo delle versioni

Le operazioni seguenti `@type` valore viene utilizzato:

Valore di @type              | Note
------------------------ | -----
PackageBaseAddress/3.0.0 | La versione iniziale

## <a name="base-url"></a>URL di base

L'URL di base per le API seguente è il valore di `@id` proprietà associato alla risorsa menzionati in precedenza `@type` valore. Nel documento seguente, il segnaposto URL di base `{@id}` verrà utilizzato.

## <a name="http-methods"></a>Metodi HTTP

Tutti gli URL trovati, il supporto di risorsa di registrazione, i metodi HTTP `GET` e `HEAD`.

## <a name="enumerate-package-versions"></a>Enumerare le versioni di pacchetto

Se il client conosce un ID pacchetto e desidera individuare quali versioni del pacchetto il pacchetto di origine è disponibile, il client può costruire un URL prevedibile per enumerare tutte le versioni di pacchetto. Questo elenco deve essere un "elenco di directory" per l'API di contenuto del pacchetto riportata di seguito.

> [!Note]
> Questo elenco contiene entrambe le versioni di pacchetto elencate e non in elenco.

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>Parametri della richiesta

nome     | In     | Tipo    | Obbligatorio | Note
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | stringa  | sì      | L'ID del pacchetto, lettere minuscole

Il `LOWER_ID` valore è l'ID del pacchetto desiderato minuscola usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.

### <a name="response"></a>Risposta

Se l'origine del pacchetto non dispone di alcuna versione dell'ID pacchetto fornito, viene restituito un codice di 404 stato.

Se l'origine del pacchetto ha una o più versioni, viene restituito un codice di 200 stato. Il corpo della risposta è un oggetto JSON con la seguente proprietà:

nome     | Tipo             | Obbligatorio | Note
-------- | ---------------- | -------- | -----
versioni | Matrice di stringhe | sì      | L'ID pacchetto

Le stringhe di `versions` matrice tutti minuscola, [normalizzare le stringhe di versione NuGet](../reference/package-versioning.md#normalized-version-numbers). Le stringhe di versione non contengono i metadati di compilazione SemVer 2.0.0.

Lo scopo è che le stringhe di versione trovate in questa matrice consente alla lettera per il `LOWER_VERSION` token, vedere i seguenti endpoint.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>Risposta di esempio

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>Scaricare il contenuto del pacchetto (.nupkg)

Se il client conosce un ID pacchetto e una versione e desidera scaricare il contenuto del pacchetto, è necessario solo costruire l'URL seguente:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>Parametri della richiesta

nome          | In     | Tipo   | Obbligatorio | Note
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | stringa | sì      | L'ID del pacchetto, lettere minuscole
LOWER_VERSION | URL    | stringa | sì      | La versione del pacchetto, normalizzato e minuscola

Entrambi `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.

Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata usando la versione NuGet [le regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers). Ciò significa che i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere escluso in questo caso.

### <a name="response-body"></a>Corpo della risposta

Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato. Il corpo della risposta sarà il contenuto del pacchetto.

Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>Risposta di esempio

Il flusso binario che è il .nupkg per 9.0.1 di newtonsoft. JSON.

## <a name="download-package-manifest-nuspec"></a>Scaricare il manifesto di pacchetto (. nuspec)

Se il client conosce un ID pacchetto e una versione e desidera scaricare il manifesto di pacchetto, è necessario solo costruire l'URL seguente:

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>Parametri della richiesta

nome          | In     | Tipo    | Obbligatorio | Note
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | stringa  | sì      | L'ID del pacchetto, lettere minuscole
LOWER_VERSION | URL    | numero intero | sì      | La versione del pacchetto, normalizzato e minuscola

Entrambi `LOWER_ID` e `LOWER_VERSION` sono minuscole usando le regole implementate da. Del NET [ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) metodo.

Il `LOWER_VERSION` è la versione del pacchetto desiderato normalizzata usando la versione NuGet [le regole di normalizzazione](../reference/package-versioning.md#normalized-version-numbers). Ciò significa che i metadati di compilazione consentiti dalla specifica SemVer 2.0.0 devono essere escluso in questo caso.

### <a name="response-body"></a>Corpo della risposta

Se il pacchetto esiste nell'origine del pacchetto, viene restituito un codice di 200 stato. Il corpo della risposta sarà il manifesto del pacchetto, ovvero il. nuspec nel .nupkg corrispondente. I. nuspec è un documento XML.

Se il pacchetto non esiste nell'origine pacchetto, viene restituito un codice di 404 stato.

### <a name="sample-request"></a>Richiesta di esempio

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>Risposta di esempio

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
