---
title: Modello di URL di report Abuse, API NuGet
description: Il modello di URL report abuse consente ai client visualizzare un collegamento nell'interfaccia utente di loro.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549339"
---
# <a name="report-abuse-url-template"></a>Modello di report abuse URL

È possibile che un client per creare un URL che può essere utilizzato dall'utente per segnalare abusi relative a un pacchetto specifico. Ciò è utile quando si vuole che il file di origine abilitare tutte le esperienze di client (anche 3rd party) delegare i report di uso improprio all'origine del pacchetto.

La risorsa usata per la creazione di questo URL è il `ReportAbuseUriTemplate` trovare la risorsa nella [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                       | Note
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La versione iniziale
ReportAbuseUriTemplate/3.0.0-rc   | Alias di `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modello di URL

L'URL per l'API seguente è il valore della `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.

## <a name="http-methods"></a>Metodi HTTP

Anche se il client non può effettuare richieste per l'URL per segnalare abusi per conto dell'utente, la pagina web deve supportare il `GET` metodo per consentire un URL selezionato essere facilmente aperto in un web browser.

## <a name="construct-the-url"></a>Creare l'URL

Dato un ID noto pacchetto e versione, l'implementazione client può creare un URL utilizzato per accedere a un'interfaccia web. L'implementazione client deve visualizzare questo URL costruito (o un collegamento selezionabile) all'utente e consente loro di aprire un web browser all'URL ed effettuare qualsiasi report abuse necessarie. L'implementazione del form report abuse è determinato dall'implementazione del server.

Il valore della `@id` è una stringa URL contenente uno dei token di segnaposto seguente:

### <a name="url-placeholders"></a>Segnaposto URL

nome        | Tipo    | Obbligatorio | Note
----------- | ------- | -------- | -----
`{id}`      | stringa  | No       | L'ID del pacchetto per segnalare abusi per
`{version}` | stringa  | No       | La versione del pacchetto per segnalare abusi per

Il `{id}` e `{version}` valori interpretato dall'implementazione del server devono essere maiuscole e minuscole e non sensibili al fatto che la versione è normalizzata.

Ad esempio, modello di uso improprio del report di nuget.org aspetto simile al seguente:

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

Se l'implementazione client deve visualizzare un collegamento al modulo di uso improprio del report per NuGet.Versioning 4.3.0, verrebbe generato l'URL seguente e offrirlo all'utente:

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
