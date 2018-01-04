---
title: Risoluzione delle controversie sui nomi dei pacchetti NuGet | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 6d664378-3f7b-426e-aef3-2254d745fe60
description: Processo per la risoluzione delle controversie tra gli autori di pacchetti NuGet correlate alla personalizzazione, ai marchi e ad altre situazioni conflittuali.
keywords: Controversie sui pacchetti NuGet, risoluzione delle controversie per NuGet, processo di risoluzione delle controversie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 32f5f766a49a2e4254a81978757d973fc5353db1
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Risoluzione delle controversie sui nomi dei pacchetti NuGet

Questo documento contiene il processo consigliato per i membri della community per la risoluzione delle controversie con altri autori di pacchetti NuGet.  

Si supponga ad esempio che Northwind Traders realizzi un sistema CRM per cui fornisce driver client sotto forma di un file MSI scaricabile dal proprio sito Web. Nancy, uno sviluppatore indipendente, intende rendere più accessibile la libreria client di Northwind e la trasforma in un pacchetto NuGet chiamato `NorthwindTraders.Client`. In un secondo momento, Northwind vuole produrre un proprio pacchetto NuGet ufficiale della libreria client e pertanto contesta la proprietà del nome del pacchetto da parte di Nancy.

In questo scenario Nancy non sembra essere animata da cattive intenzioni, ma supporta gli strumenti e i clienti di Northwind offrendo il proprio contributo in termini di tempo e codice. Allo stesso tempo, Northwind è il legittimo proprietario del nome Northwind.

Seguendo il processo riportato di seguito, Northwind e Nancy possono collaborare a una risoluzione appropriata, perché entrambi sono interessati a offrire il proprio contributo alla community di sviluppatori. Di solito non è necessario che il team di NuGet sia coinvolto, in genere la collaborazione è la scelta migliore. In effetti, tutte le controversie portate finora all'attenzione del team di NuGet sono state risolte senza che il team abbia dovuto esprimere il suo giudizio.


## <a name="process"></a>Processo

1. Contattare i proprietari del pacchetto per cui è sorta la controversia usando il collegamento **Contact Owners** (Contatta proprietari) nella pagina dei dettagli del pacchetto. Spiegare il problema in modo diretto e cortese.
2. Inviare una copia del messaggio all'indirizzo [support@nuget.org](mailto:support@nuget.org) in modo che NuGet e .NET Foundation siano al corrente della controversia.
3. Attendere un massimo di 30 giorni per la risoluzione, dopodiché segnalare nuovamente il problema all'indirizzo [support@nuget.org](mailto:support@nuget.org). Il team di supporto di nuget.org verrà contattato e tenterà di risolvere la controversia collaborando con entrambe le parti.
