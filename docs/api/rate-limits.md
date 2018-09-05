---
title: Limiti, API NuGet di velocità
description: I limiti di velocità per impedirne l'uso improprio verrà applicata APIs di NuGet.
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548677"
---
# <a name="rate-limits"></a>Limiti di velocità

L'API di NuGet.org consente di applicare la limitazione della frequenza per impedirne l'uso improprio. Le richieste che superano il limite di frequenza restituiranno l'errore seguente: 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

Oltre a utilizzando i limiti di velocità di limitazione delle richieste, alcune API applicano anche quota. Le richieste che superano la quota di restituiranno l'errore seguente:

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

Le tabelle seguenti elencano i limiti di velocità per l'API di NuGet.org.

## <a name="package-search"></a>Ricerca di un pacchetto

> [!Note]
> È consigliabile usare di NuGet.org [V3 API](https://docs.microsoft.com/nuget/api/search-query-service-resource) per la ricerca ad alte prestazioni e non siano presenti limitare attualmente. Per versioni V1 e V2 API di ricerca, si applicano i limiti followins:


| API | Tipo di limite | Valore del limite | API usecase |
|:---|:---|:---|:---|
**OTTIENI** `/api/v1/Packages` | IP | 1000 al minuto | Eseguire query sui metadati del pacchetto NuGet tramite OData v1 `Packages` raccolta |
**OTTIENI** `/api/v1/Search()` | IP | 3000 / minuto | Cercare i pacchetti NuGet tramite l'endpoint ricerca v1 | 
**OTTIENI** `/api/v2/Packages` | IP | 20000 al minuto | Eseguire query sui metadati del pacchetto NuGet tramite OData v2 `Packages` raccolta | 
**OTTIENI** `/api/v2/Packages/$count` | IP | 100 al minuto | Numero di pacchetti NuGet tramite OData v2 di query `Packages` raccolta | 

## <a name="package-push-and-unlist"></a>Pacchetto di effettuare il Push e rimuovere dall'elenco

| API | Tipo di limite | Valore del limite | API usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | Chiave API | 250 / ora | Caricare un nuovo pacchetto NuGet (versione) tramite l'endpoint v2 push 
**DELETE** `/api/v2/package/{id}/{version}` | Chiave API | 250 / ora | Rimuovere un pacchetto NuGet (versione) tramite l'endpoint v2 
