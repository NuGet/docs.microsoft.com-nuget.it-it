---
title: Limiti di velocità, API NuGet
description: Le API NuGet avranno limiti di velocità applicati per impedire abusi.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367934"
---
# <a name="rate-limits"></a>Limiti di velocità

L'API NuGet.org impone la limitazione della frequenza per impedire abusi. Le richieste che superano il limite di frequenza restituiscono l'errore seguente: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Oltre alla limitazione delle richieste con limiti di velocità, alcune API applicano anche la quota. Le richieste che superano la quota restituiscono l'errore seguente:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Le tabelle seguenti elencano i limiti di velocità per l'API NuGet.org.

## <a name="package-search"></a>Ricerca di pacchetti

> [!Note]
> Si consiglia di usare le API di [ricerca V3](search-query-service-resource.md) di NuGet. org, perché attualmente non è limitato. Per le API di ricerca V1 e V2, si applicano i limiti seguenti:

| API | Tipo limite | Valore limite | Caso di utilizzo dell'API |
|:---|:---|:---|:---|
**Ottenere**`/api/v1/Packages` | IP | 1000 al minuto | Eseguire query sui metadati del pacchetto NuGet tramite la raccolta OData V1 `Packages` |
**Ottenere**`/api/v1/Search()` | IP | 3000 al minuto | Cerca i pacchetti NuGet tramite l'endpoint di ricerca V1 | 
**Ottenere**`/api/v2/Packages` | IP | 20000 al minuto | Eseguire query sui metadati del pacchetto NuGet tramite la raccolta OData v2 `Packages` | 
**Ottenere**`/api/v2/Packages/$count` | IP | 100 al minuto | Eseguire query sul numero di pacchetti NuGet tramite la raccolta OData v2 `Packages` | 

## <a name="package-push-and-unlist"></a>Push e Unlist di pacchetti

| API | Tipo limite | Valore limite | Caso di utilizzo dell'API | 
|:---|:---|:---|:--- |
**Inserisci**`/api/v2/package` | API key | 350/ora | Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push V2 
**Elimina**`/api/v2/package/{id}/{version}` | API key | 250/ora | Non elencare un pacchetto NuGet (versione) tramite l'endpoint V2 

## <a name="nugetorg-website-page-views"></a>Visualizzazioni delle pagine del sito Web nuget.org

Se si accede alle pagine Web di nuget.org a livello di codice, è consigliabile esaminare le [API V3](overview.md)documentate. Questi endpoint consentono un accesso più semplice ai metadati e al contenuto del pacchetto. L'API V3 offre una maggiore disponibilità e offre prestazioni migliori rispetto all'accesso alle pagine Web della raccolta NuGet, progettate per l'interazione con il Web browser.

| API | Tipo limite | Valore limite | Caso di utilizzo dell'API | 
|:---|:---|:---|:--- |
**Ottenere**`/package/{id}/{version}` | IP | 50 al minuto | Visualizza la pagina dei dettagli del pacchetto (versione). 
