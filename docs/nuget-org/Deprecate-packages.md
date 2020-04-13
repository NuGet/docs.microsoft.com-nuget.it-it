---
title: Deprecazione dei pacchetti su nuget.org
description: Descrizione dettagliata del processo di deprecazione dei pacchetti e del modo in cui i client mostrano queste informazioni
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/07/2020
ms.locfileid: "74096875"
---
# <a name="deprecating-packages"></a>Pacchetti deprecati

È possibile deprecare un pacchetto se non si gestisce più un pacchetto o se si desidera incoraggiare i consumer del pacchetto a passare a un altro pacchetto. 

La deprecazione del pacchetto è diversa **dall'annullamento dell'elenco** del pacchetto, come spiegato di seguito:Package deprecation is different than unlisting your package as explained below:
* **L'annullamento dell'elenco** di un pacchetto ne impedisce l'individuazione perché è nascosto nei risultati della ricerca. 
* **La deprecazione di** un pacchetto consente ai consumer esistenti del pacchetto di scoprire se è installato o utilizzato nei progetti. Consente inoltre di conoscere il motivo della deprecazione e di un pacchetto consigliato alternativo come specificato dall'utente (l'autore del pacchetto). La deprecazione di un pacchetto non annulla l'elenco del pacchetto. 

In qualità di editore, puoi scegliere di annullare l'elenco e di deprecare i pacchetti.

## <a name="deprecation-workflow"></a>Flusso di lavoro di deprecazione
1. Per deprecare un pacchetto, vai a **Gestisci pacchetti** e seleziona **Deprecation:**

    ![Vai all'opzione del pacchetto deprecatoGo to deprecate package option](media/deprecation-select-option.png)

2. Selezionare la versione che si desidera deprecare. Se si desidera deprecare tutte le versioni, scegliere **l'opzione Seleziona tutte le versioni.**

    ![Selezionare le versioni del pacchetto da deprecareSelect package versions to deprecate](media/deprecation-select-version.png)

3. Scegliere un motivo per la deprecazione. Se il pacchetto non viene più mantenuto, scegliere l'opzione **Legacy.** Se la versione specifica ha un bug critico, scegliere l'opzione **ha bug critici.** Per qualsiasi altro motivo, selezionare **Altro**. È sempre possibile specificare un pacchetto (e una versione) consigliato alternativo e un messaggio personalizzato ai proprietari. 

    ![Selezionare i motivi alternativi di raccomandazione del pacchetto e il messaggio personalizzato](media/deprecation-save.png)

> [!Note]
> Il messaggio personalizzato viene visualizzato solo nuget.org ma non dai client. Attualmente, i `dotnet.exe` client, ad esempio e NuGet Gestione pacchetti non viene visualizzato il messaggio personalizzato.

## <a name="client-experience-for-deprecated-packages"></a>Esperienza client per i pacchetti deprecatiClient experience for deprecated packages
Una volta che un pacchetto è stato deprecato, i relativi consumer vengono informati su di esso nei modi seguenti (a seconda del client utilizzato).

### <a name="visual-studio"></a>Visual Studio 
*Disponibile a partire da Visual Studio 2019 versione 16.3*

Visual Studio segnala l'utilizzo di un `Installed` pacchetto deprecato nella scheda. Verrà visualizzato un avviso per il pacchetto e le relative informazioni sulla deprecazione (incluso il motivo per cui è stato deprecato e il pacchetto alternativo da utilizzare, se presente).

   ![Pacchetti deprecati nella scheda Visual Studio installato di Gestione pacchetti](media/deprecation-vs.png)

### <a name="dotnetexe"></a>dotnet.exe
*Disponibile a partire da .NET SDK 3.0*

Se si utilizza dotnet.exe, è `dotnet list package --deprecated` possibile eseguire il comando nella cartella della soluzione o del progetto per ottenere un elenco di pacchetti deprecati insieme alle informazioni sulla deprecazione:

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
