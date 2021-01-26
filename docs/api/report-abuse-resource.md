---
title: Modello di URL di abuso report, API NuGet
description: Il modello report abuse URL consente ai client di visualizzare un collegamento Segnala abusi nell'interfaccia utente.
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775227"
---
# <a name="report-abuse-url-template"></a>Modello di URL di report abusi

È possibile che un client crei un URL che può essere usato dall'utente per segnalare gli abusi relativi a un pacchetto specifico. Questa operazione è utile quando un'origine del pacchetto vuole abilitare tutte le esperienze client (anche di terze parti) per delegare i report sugli abusi all'origine del pacchetto.

La risorsa utilizzata per la compilazione di questo URL è la `ReportAbuseUriTemplate` risorsa presente nell' [indice del servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

`@type`Vengono usati i valori seguenti:

Valore della proprietà @type                       | Note
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | Versione iniziale
ReportAbuseUriTemplate/3.0.0-RC   | Alias di `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modello di URL

L'URL per l'API seguente è il valore della `@id` proprietà associata a uno dei valori di risorsa `@type` indicati sopra.

## <a name="http-methods"></a>Metodi HTTP

Anche se il client non è destinato a eseguire richieste all'URL del report abusi per conto dell'utente, la pagina Web deve supportare il `GET` metodo per consentire l'apertura semplice di un URL selezionato in un Web browser.

## <a name="construct-the-url"></a>Costruire l'URL

Dato un ID e una versione del pacchetto noti, l'implementazione client può costruire un URL usato per accedere a un'interfaccia Web. L'implementazione client deve visualizzare l'URL costruito (o collegamento selezionabile) per consentire all'utente di aprire un Web browser all'URL e di apportare eventuali segnalazioni di abusi necessarie. L'implementazione del modulo report di abusi è determinata dall'implementazione del server.

Il valore di `@id` è una stringa URL che contiene i token segnaposto seguenti:

### <a name="url-placeholders"></a>Segnaposto URL

Nome        | Type    | Necessario | Note
----------- | ------- | -------- | -----
`{id}`      | string  | no       | ID del pacchetto per segnalare gli abusi per
`{version}` | string  | no       | Versione del pacchetto per cui segnalare gli abusi

I `{id}` `{version}` valori e interpretati dall'implementazione del server non devono fare distinzione tra maiuscole e minuscole e non sono sensibili alla normalizzazione della versione.

Il modello di abusi dei report di NuGet. org, ad esempio, ha un aspetto simile al seguente:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Se l'implementazione client deve visualizzare un collegamento al modulo segnalazione abusi per NuGet. Versioning 4.3.0, produrrebbe l'URL seguente e lo fornirà all'utente:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
