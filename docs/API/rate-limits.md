---
title: Limiti di velocità | Documenti Microsoft
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: APIs NuGet verranno sono applicati i limiti di velocità per evitare abusi.
keywords: Limitazione di velocità NuGet API,
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2018
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
**GET** `/api/v1/Packages` | IP | 1000 / minuto | Eseguire una query dei metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta |
**GET** `/api/v1/Search()` | IP | 3000 / minuto | Ricerca per i pacchetti NuGet tramite l'endpoint di ricerca v1 | 
**GET** `/api/v2/Packages` | IP | 20000 / minuto | Eseguire una query dei metadati del pacchetto NuGet tramite v2 OData `Packages` raccolta | 
**GET** `/api/v2/Packages/$count` | IP | 100 / minuto | Eseguire una query conteggio pacchetto NuGet tramite v2 OData `Packages` raccolta | 

## <a name="package-push-and-unlist"></a>Pacchetto Push ed esclusione

| API | Tipo di limite | Valore del limite | APU usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Chiave API | 100 / minuto | Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint di push v2 
**ELIMINARE** `/api/v2/package/{id}/{version}` | Chiave API | 100 / minuto | Esclusione di un pacchetto NuGet (versione) tramite l'endpoint v2 
