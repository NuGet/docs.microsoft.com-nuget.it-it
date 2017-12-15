---
title: Il modello di URL abuso, NuGet API di report | Documenti Microsoft
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
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: Modello di URL del report abuso consente ai client di visualizzare un collegamento nell'interfaccia utente di loro.
keywords: Per segnalare abusi API NuGet, reclamo API NuGet, modello di URL di report NuGet.org
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a>Modello di URL di report abusi

È possibile che un client generare un URL che può essere utilizzato dall'utente per segnalare abusi su un pacchetto specifico. Ciò è utile quando si desidera abilitare tutte le esperienze di client (parte 3 anche) delegare abuso report all'origine del pacchetto un'origine del pacchetto.

La risorsa utilizzata per il recupero di contenuto del pacchetto è il `ReportAbuseUriTemplate` risorse, vedere il [indice servizio](service-index.md).

## <a name="versioning"></a>Controllo delle versioni

Nell'esempio `@type` vengono utilizzati i valori:

Valore di @type                       | Note
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | La versione iniziale
ReportAbuseUriTemplate/3.0.0-rc   | Alias di`ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>Modello di URL

L'URL per l'API seguente è il valore di `@id` proprietà associati a uno della risorsa menzionati in precedenza `@type` valori.

## <a name="http-methods"></a>Metodi HTTP

Anche se il client non può effettuare richieste all'URL di abuso del report per conto dell'utente, la pagina web deve supportare il `GET` metodo per consentire a un URL da aprire facilmente in un web browser si fa clic.

## <a name="construct-the-url"></a>Costruire l'URL

Dato un ID pacchetto noti e una versione, l'implementazione del client può costruire un URL utilizzato per accedere a un'interfaccia web. L'implementazione del client deve essere visualizzato questo URL costruito (o un collegamento ipertestuale) all'utente consentendo di aprire un web browser all'URL e qualsiasi relazione abuso necessarie. L'implementazione del modulo report abuso viene determinata dall'implementazione del server.

Il valore di `@id` è una stringa URL contenente uno dei token di segnaposto seguente:

### <a name="url-placeholders"></a>Segnaposto URL

Nome        | Tipo    | Obbligatorio | Note
----------- | ------- | -------- | -----
`{id}`      | string  | No       | L'ID del pacchetto per segnalare abusi per
`{version}` | string  | No       | La versione del pacchetto per segnalare abusi per

Il `{id}` e `{version}` valori dall'implementazione del server devono essere insenstive case e non sensibili se la versione è normalizzato.

Ad esempio, modello di abuso di nuget.org report simile al seguente:

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

Se l'implementazione del client deve visualizzare un collegamento al modulo di abuso del report per NuGet.Versioning 4.3.0, verrebbe generato l'URL seguente e che sia disponibile per l'utente:

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```