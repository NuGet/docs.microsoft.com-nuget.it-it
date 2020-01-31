---
title: Modello di URL dei dettagli del pacchetto, API NuGet
description: Il modello di URL dei dettagli del pacchetto consente ai client di visualizzare nell'interfaccia utente un collegamento Web a più dettagli del pacchetto
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812935"
---
# <a name="package-details-url-template"></a>Modello URL Dettagli pacchetto

È possibile che un client crei un URL che può essere usato dall'utente per visualizzare altri dettagli del pacchetto nel Web browser. Questa operazione è utile quando un'origine del pacchetto desidera visualizzare informazioni aggiuntive su un pacchetto che potrebbero non rientrare nell'ambito di ciò che viene visualizzato nell'applicazione client NuGet.

La risorsa usata per la compilazione di questo URL è la risorsa `PackageDetailsUriTemplate` trovata nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Versionamento

Vengono utilizzati i valori `@type` seguenti:

Valore di @type                     | Note
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | Versione iniziale

## <a name="url-template"></a>Modello URL

L'URL per l'API seguente è il valore della proprietà `@id` associata a uno dei valori di `@type` di risorse indicati sopra.

## <a name="http-methods"></a>Metodi HTTP

Anche se il client non è destinato a eseguire richieste all'URL dei dettagli del pacchetto per conto dell'utente, la pagina Web deve supportare il metodo `GET` per consentire l'apertura semplice di un URL selezionato in un Web browser.

## <a name="construct-the-url"></a>Costruire l'URL

Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web. L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di ottenere ulteriori informazioni sul pacchetto. Il contenuto della pagina dei dettagli del pacchetto è determinato dall'implementazione del server.

L'URL deve essere un URL assoluto e lo schema (protocollo) deve essere HTTPS.

Il valore della `@id` nell'indice del servizio è una stringa URL contenente uno dei token segnaposto seguenti:

### <a name="url-placeholders"></a>Segnaposto URL

Name        | Tipo di    | Richiesto | Note
----------- | ------- | -------- | -----
`{id}`      | string  | No       | ID del pacchetto per cui ottenere i dettagli
`{version}` | string  | No       | Versione del pacchetto per cui ottenere i dettagli

Il server deve accettare `{id}` e `{version}` valori con qualsiasi combinazione di maiuscole e minuscole. Inoltre, il server non deve essere sensibile alla [normalizzazione](../concepts/package-versioning.md#normalized-version-numbers)della versione. In altre parole, il server deve accettare anche versioni non normalizzate.

Ad esempio, il modello di dettagli del pacchetto NuGet. org è simile al seguente:

    https://www.nuget.org/packages/{id}/{version}

Se l'implementazione client deve visualizzare un collegamento ai dettagli del pacchetto per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
