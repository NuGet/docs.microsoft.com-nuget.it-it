---
title: Modello di URL dettagli del pacchetto, NuGet API
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare l'interfaccia utente web collegamento a ulteriori dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638074"
---
# <a name="package-details-url-template"></a>Modello di URL dei dettagli del pacchetto

È possibile che un client per creare un URL che può essere utilizzato dall'utente per visualizzare ulteriori dettagli del pacchetto nel web browser. Ciò è utile quando si desidera visualizzare informazioni aggiuntive relative a un pacchetto che potrebbe non rientrare nell'ambito di ciò che l'applicazione client di NuGet Mostra un'origine del pacchetto.

La risorsa usata per la creazione di questo URL è il `PackageDetailsUriTemplate` trovare la risorsa nella [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                     | Note
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | La versione iniziale

## <a name="url-template"></a>Modello di URL

L'URL per l'API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.

## <a name="http-methods"></a>Metodi HTTP

Anche se il client non può effettuare richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina web deve supportare il `GET` metodo per consentire un URL selezionato essere facilmente aperto in un web browser.

## <a name="construct-the-url"></a>Creare l'URL

Dato un ID noto pacchetto e versione, l'implementazione client può creare un URL utilizzato per accedere a un'interfaccia web. L'implementazione client deve visualizzare questo URL costruito (o un collegamento selezionabile) all'utente e consente loro di aprire un web browser all'URL e per altre informazioni sul pacchetto. Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.

L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.

Il valore della `@id` nel servizio di indice è una stringa URL contenente uno dei token di segnaposto seguente:

### <a name="url-placeholders"></a>Segnaposto URL

Nome        | Tipo    | Obbligatorio | Note
----------- | ------- | -------- | -----
`{id}`      | string  | No       | L'ID del pacchetto per ottenere i dettagli per
`{version}` | string  | No       | La versione del pacchetto per ottenere i dettagli per

Il server deve accettare `{id}` e `{version}` valori con qualsiasi maiuscole e minuscole. Inoltre, il server non deve essere sensibile alle se è la versione [normalizzato](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers). In altre parole, il server deve accettare accettano anche le versioni non normalizzato.

Ad esempio, modello di dettagli del pacchetto di nuget.org aspetto simile al seguente:

    https://www.nuget.org/packages/{id}/{version}

Se l'implementazione client deve visualizzare un collegamento per i dettagli del pacchetto per NuGet.Versioning 4.3.0, verrebbe generato l'URL seguente e offrirlo all'utente:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
