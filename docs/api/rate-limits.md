---
title: Limiti, NuGet API di velocità
description: APIs NuGet verranno sono applicati i limiti di velocità per evitare abusi.
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/17/2018
---
# <a name="rate-limits"></a>Limiti di velocità

L'API di NuGet.org impone limiti di velocità per evitare di evitare eventuali abusi. Le richieste che superano il limite di velocità restituiranno l'errore seguente: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.

## <a name="package-search"></a>Ricerca di pacchetto

> [!Note]
> Si consiglia di usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non hanno alcun limite attualmente. Per le versioni V1 e V2 le API di ricerca, applicano i limiti followins:


| API | Tipo di limite | Valore del limite | API usecase |
|:---|:---|:---|:---|
**OTTIENI** `/api/v1/Packages` | IP | 1000 / minuto | Eseguire una query dei metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta |
**OTTIENI** `/api/v1/Search()` | IP | 3000 / minuto | Ricerca per i pacchetti NuGet tramite l'endpoint di ricerca v1 | 
**OTTIENI** `/api/v2/Packages` | IP | 20000 / minuto | Eseguire una query dei metadati del pacchetto NuGet tramite v2 OData `Packages` raccolta | 
**OTTIENI** `/api/v2/Packages/$count` | IP | 100 / minuto | Eseguire una query conteggio pacchetto NuGet tramite v2 OData `Packages` raccolta | 

## <a name="package-push-and-unlist"></a>Pacchetto Push ed esclusione

| API | Tipo di limite | Valore del limite | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Chiave API | 250 / ora | Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push v2 
**ELIMINARE** `/api/v2/package/{id}/{version}` | Chiave API | 250 / ora | Esclusione di un pacchetto NuGet (versione) tramite l'endpoint v2 
