---
title: Risoluzione delle controversie sui nomi dei pacchetti NuGet
description: Processo per la risoluzione delle controversie tra gli autori di pacchetti NuGet correlate alla personalizzazione, ai marchi e ad altre situazioni conflittuali.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426936"
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Risoluzione delle controversie sui nomi dei pacchetti NuGet

Questo articolo presenta il processo consigliato ai membri della community per la risoluzione delle controversie con altri autori di pacchetti NuGet.

Si supponga ad esempio che Northwind Traders realizzi un sistema CRM per cui fornisce driver client sotto forma di un file MSI scaricabile dal proprio sito Web. Nancy, uno sviluppatore indipendente, intende rendere più accessibile la libreria client di Northwind e la trasforma in un pacchetto NuGet chiamato `NorthwindTraders.Client`. In un secondo momento, Northwind vuole produrre un proprio pacchetto NuGet ufficiale della libreria client e pertanto contesta la proprietà del nome del pacchetto da parte di Nancy.

In questo scenario Nancy non sembra essere animata da cattive intenzioni, ma supporta gli strumenti e i clienti di Northwind offrendo il proprio contributo in termini di tempo e codice. Allo stesso tempo, Northwind è il legittimo proprietario del nome Northwind.

Seguendo il processo riportato di seguito, Northwind e Nancy possono collaborare a una risoluzione appropriata, perché entrambi sono interessati a offrire il proprio contributo alla community di sviluppatori. Di solito non è necessario che il team di NuGet sia coinvolto, in genere la collaborazione è la scelta migliore. In effetti, tutte le controversie portate finora all'attenzione del team di NuGet sono state risolte senza che il team abbia dovuto esprimere il suo giudizio.

## <a name="process"></a>Process

1. Contattare i proprietari del pacchetto oggetto della disputa usando il collegamento **Contact Owners** (Contatta proprietari) disponibile nella pagina dei dettagli del pacchetto. Spiegare il problema in un modo cortese e diretto.
2. Inviare una copia [support@nuget.org](mailto:support@nuget.org) del messaggio in modo che NuGet e .NET Foundation siano a conoscenza della controversia.
3. Attendi un massimo di 30 giorni [support@nuget.org](mailto:support@nuget.org) per una risoluzione, quindi invia di nuovo una notifica. Il team di supporto di nuget.org verrà contattato e tenterà di risolvere la controversia collaborando con entrambe le parti.
