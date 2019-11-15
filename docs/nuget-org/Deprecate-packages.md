---
title: Deprecazione dei pacchetti in nuget.org
description: Descrizione dettagliata del processo di deprecazione dei pacchetti e del modo in cui i client visualizzano queste informazioni
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096875"
---
# <a name="deprecating-packages"></a>Deprecazione dei pacchetti

È possibile deprecare un pacchetto se non si gestisce più un pacchetto o se si vuole incoraggiare i consumer del pacchetto a passare a un altro pacchetto. 

La deprecazione del pacchetto è diversa dall'annullamento dell' **elenco** del pacchetto, come illustrato di seguito:
* L' **unlisting** di un pacchetto impedisce l'individuazione perché è nascosta nei risultati della ricerca. 
* La **deprecazione** di un pacchetto consente ai consumer esistenti del pacchetto di scoprire se sono installati o usati nei progetti. Consente inoltre di comprendere il motivo della deprecazione e un pacchetto alternativo consigliato come specificato dall'utente (editore del pacchetto). La deprecazione di un pacchetto non comporta l'annullamento dell'elenco del pacchetto. 

Come server di pubblicazione, è possibile scegliere di non elencare i pacchetti e deprecarli.

## <a name="deprecation-workflow"></a>Flusso di lavoro di deprecazione
1. Per deprecare un pacchetto, passare a **Gestisci pacchetti** e selezionare **deprecazione**:

    ![Opzione Vai a deprecate Package](media/deprecation-select-option.png)

2. Selezionare la versione che si desidera deprecare. Se si desidera deprecare tutte le versioni, scegliere l'opzione **Seleziona tutte le versioni** .

    ![Selezionare le versioni del pacchetto da deprecare](media/deprecation-select-version.png)

3. Scegliere un motivo per la deprecazione. Se il pacchetto non viene più mantenuto, scegliere l'opzione **legacy** . Se la versione specifica presenta un bug critico, scegliere l'opzione **con i bug critici** . Per qualsiasi altro motivo, selezionare **altro**. È sempre possibile specificare un pacchetto (e una versione) consigliato alternativo e un messaggio personalizzato per i proprietari. 

    ![Select reasons alternative Package Recommendation e Custom Message](media/deprecation-save.png)

> [!Note]
> Il messaggio personalizzato viene visualizzato solo in nuget.org ma non dai client. Attualmente, i client come `dotnet.exe` e gestione pacchetti NuGet non visualizzano il messaggio personalizzato.

## <a name="client-experience-for-deprecated-packages"></a>Esperienza client per Pacchetti deprecati
Una volta che un pacchetto è stato deprecato, i relativi consumer riceveranno una notifica nei modi seguenti, a seconda del client usato.

### <a name="visual-studio"></a>Visual Studio 
*Disponibile a partire da Visual Studio 2019 versione 16,3*

In Visual Studio viene visualizzato un avviso relativo all'utilizzo di un pacchetto deprecato nella scheda `Installed`. Verrà visualizzato un avviso per il pacchetto e le relative informazioni di deprecazione (incluso il motivo per cui è stato deprecato e il pacchetto alternativo da usare, se presente).

   ![Pacchetti deprecati nella scheda installato di Visual Studio di gestione pacchetti](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet. exe
*Disponibile a partire da .NET SDK 3,0*

Se si utilizza dotnet. exe, è possibile eseguire il comando `dotnet list package --deprecated` nella cartella della soluzione o del progetto per ottenere un elenco di Pacchetti deprecati insieme alle informazioni di deprecazione:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
