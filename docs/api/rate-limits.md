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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813195"
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

| API | Tipo limite | Valore limite | API useCase |
|:---|:---|:---|:---|
**Ottenere** `/api/v1/Packages` | IP | 1000 al minuto | Eseguire query sui metadati del pacchetto NuGet tramite la raccolta di `Packages` OData V1 |
**Ottenere** `/api/v1/Search()` | IP | 3000 al minuto | Cerca i pacchetti NuGet tramite l'endpoint di ricerca V1 | 
**Ottenere** `/api/v2/Packages` | IP | 20000 al minuto | Eseguire query sui metadati del pacchetto NuGet tramite la raccolta `Packages` OData V2 | 
**Ottenere** `/api/v2/Packages/$count` | IP | 100 al minuto | Eseguire query sul numero di pacchetti NuGet tramite la raccolta `Packages` OData V2 | 

## <a name="package-push-and-unlist"></a>Push e Unlist di pacchetti

| API | Tipo limite | Valore limite | API useCase | 
|:---|:---|:---|:--- |
**Inserisci** `/api/v2/package` | Chiave API | 350/ora | Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push V2 
**Elimina** `/api/v2/package/{id}/{version}` | Chiave API | 250/ora | Non elencare un pacchetto NuGet (versione) tramite l'endpoint V2 
