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
# <a name="deprecating-packages"></a><span data-ttu-id="306f4-103">Pacchetti deprecati</span><span class="sxs-lookup"><span data-stu-id="306f4-103">Deprecating packages</span></span>

<span data-ttu-id="306f4-104">È possibile deprecare un pacchetto se non si gestisce più un pacchetto o se si desidera incoraggiare i consumer del pacchetto a passare a un altro pacchetto.</span><span class="sxs-lookup"><span data-stu-id="306f4-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="306f4-105">La deprecazione del pacchetto è diversa **dall'annullamento dell'elenco** del pacchetto, come spiegato di seguito:Package deprecation is different than unlisting your package as explained below:</span><span class="sxs-lookup"><span data-stu-id="306f4-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="306f4-106">**L'annullamento dell'elenco** di un pacchetto ne impedisce l'individuazione perché è nascosto nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="306f4-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="306f4-107">**La deprecazione di** un pacchetto consente ai consumer esistenti del pacchetto di scoprire se è installato o utilizzato nei progetti.</span><span class="sxs-lookup"><span data-stu-id="306f4-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="306f4-108">Consente inoltre di conoscere il motivo della deprecazione e di un pacchetto consigliato alternativo come specificato dall'utente (l'autore del pacchetto).</span><span class="sxs-lookup"><span data-stu-id="306f4-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="306f4-109">La deprecazione di un pacchetto non annulla l'elenco del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="306f4-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="306f4-110">In qualità di editore, puoi scegliere di annullare l'elenco e di deprecare i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="306f4-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="306f4-111">Flusso di lavoro di deprecazione</span><span class="sxs-lookup"><span data-stu-id="306f4-111">Deprecation workflow</span></span>
1. <span data-ttu-id="306f4-112">Per deprecare un pacchetto, vai a **Gestisci pacchetti** e seleziona **Deprecation:**</span><span class="sxs-lookup"><span data-stu-id="306f4-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Vai all'opzione del pacchetto deprecatoGo to deprecate package option](media/deprecation-select-option.png)

2. <span data-ttu-id="306f4-114">Selezionare la versione che si desidera deprecare.</span><span class="sxs-lookup"><span data-stu-id="306f4-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="306f4-115">Se si desidera deprecare tutte le versioni, scegliere **l'opzione Seleziona tutte le versioni.**</span><span class="sxs-lookup"><span data-stu-id="306f4-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Selezionare le versioni del pacchetto da deprecareSelect package versions to deprecate](media/deprecation-select-version.png)

3. <span data-ttu-id="306f4-117">Scegliere un motivo per la deprecazione.</span><span class="sxs-lookup"><span data-stu-id="306f4-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="306f4-118">Se il pacchetto non viene più mantenuto, scegliere l'opzione **Legacy.**</span><span class="sxs-lookup"><span data-stu-id="306f4-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="306f4-119">Se la versione specifica ha un bug critico, scegliere l'opzione **ha bug critici.**</span><span class="sxs-lookup"><span data-stu-id="306f4-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="306f4-120">Per qualsiasi altro motivo, selezionare **Altro**.</span><span class="sxs-lookup"><span data-stu-id="306f4-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="306f4-121">È sempre possibile specificare un pacchetto (e una versione) consigliato alternativo e un messaggio personalizzato ai proprietari.</span><span class="sxs-lookup"><span data-stu-id="306f4-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Selezionare i motivi alternativi di raccomandazione del pacchetto e il messaggio personalizzato](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="306f4-123">Il messaggio personalizzato viene visualizzato solo nuget.org ma non dai client.</span><span class="sxs-lookup"><span data-stu-id="306f4-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="306f4-124">Attualmente, i `dotnet.exe` client, ad esempio e NuGet Gestione pacchetti non viene visualizzato il messaggio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="306f4-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="306f4-125">Esperienza client per i pacchetti deprecatiClient experience for deprecated packages</span><span class="sxs-lookup"><span data-stu-id="306f4-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="306f4-126">Una volta che un pacchetto è stato deprecato, i relativi consumer vengono informati su di esso nei modi seguenti (a seconda del client utilizzato).</span><span class="sxs-lookup"><span data-stu-id="306f4-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="306f4-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="306f4-127">Visual Studio</span></span> 
<span data-ttu-id="306f4-128">*Disponibile a partire da Visual Studio 2019 versione 16.3*</span><span class="sxs-lookup"><span data-stu-id="306f4-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="306f4-129">Visual Studio segnala l'utilizzo di un `Installed` pacchetto deprecato nella scheda. Verrà visualizzato un avviso per il pacchetto e le relative informazioni sulla deprecazione (incluso il motivo per cui è stato deprecato e il pacchetto alternativo da utilizzare, se presente).</span><span class="sxs-lookup"><span data-stu-id="306f4-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Pacchetti deprecati nella scheda Visual Studio installato di Gestione pacchetti](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="306f4-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="306f4-131">dotnet.exe</span></span>
<span data-ttu-id="306f4-132">*Disponibile a partire da .NET SDK 3.0*</span><span class="sxs-lookup"><span data-stu-id="306f4-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="306f4-133">Se si utilizza dotnet.exe, è `dotnet list package --deprecated` possibile eseguire il comando nella cartella della soluzione o del progetto per ottenere un elenco di pacchetti deprecati insieme alle informazioni sulla deprecazione:</span><span class="sxs-lookup"><span data-stu-id="306f4-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
