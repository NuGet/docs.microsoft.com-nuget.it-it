---
title: Modello di URL dei dettagli del pacchetto, API NuGet
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare nell'interfaccia utente un collegamento Web a più dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488172"
---
# <a name="package-details-url-template"></a>Modello URL Dettagli pacchetto

È possibile che un client crei un URL che può essere usato dall'utente per visualizzare altri dettagli del pacchetto nel Web browser. Questa operazione è utile quando un'origine del pacchetto desidera visualizzare informazioni aggiuntive su un pacchetto che potrebbero non rientrare nell'ambito di ciò che viene visualizzato nell'applicazione client NuGet.

La risorsa utilizzata per la compilazione di questo URL `PackageDetailsUriTemplate` è la risorsa presente nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Vengono usati `@type` i valori seguenti:

Valore di @type                     | Note
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Versione iniziale

## <a name="url-template"></a>Modello URL

L'URL per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` indicati sopra.

## <a name="http-methods"></a>Metodi HTTP

Anche se il client non è destinato a eseguire richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina Web deve supportare `GET` il metodo per consentire l'apertura semplice di un URL selezionato in un Web browser.

## <a name="construct-the-url"></a>Costruire l'URL

Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web. L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di ottenere ulteriori informazioni sul pacchetto. Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.

L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.

Il valore di `@id` nell'indice del servizio è una stringa URL contenente uno dei token segnaposto seguenti:

### <a name="url-placeholders"></a>Segnaposto URL

Name        | Type    | Obbligatoria | Note
----------- | ------- | -------- | -----
`{id}`      | string  | no       | ID del pacchetto per cui ottenere i dettagli
`{version}` | string  | no       | Versione del pacchetto per cui ottenere i dettagli

Il server deve accettare `{id}` i `{version}` valori e con qualsiasi combinazione di maiuscole e minuscole. Inoltre, il server non deve essere sensibile alla [normalizzazione](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers)della versione. In altre parole, il server deve accettare anche versioni non normalizzate.

Ad esempio, il modello di dettagli del pacchetto NuGet. org è simile al seguente:

    https://www.nuget.org/packages/{id}/{version}

Se l'implementazione client deve visualizzare un collegamento ai dettagli del pacchetto per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
