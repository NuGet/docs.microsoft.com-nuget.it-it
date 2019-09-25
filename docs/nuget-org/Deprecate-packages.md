---
title: Deprecazione dei pacchetti in nuget.org
description: Descrizione dettagliata del processo di deprecazione dei pacchetti e del modo in cui i client visualizzano queste informazioni
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 120b463fda856fe9dd407b6eba32d60e0918f763
ms.sourcegitcommit: 188ade66b7ac807ba1667c77cfb9325bf89a8a4a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2019
ms.locfileid: "71248897"
---
# <a name="deprecating-packages"></a><span data-ttu-id="9b074-103">Deprecazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="9b074-103">Deprecating packages</span></span>

<span data-ttu-id="9b074-104">È possibile deprecare un pacchetto se non si gestisce più un pacchetto o se si vuole incoraggiare i consumer del pacchetto a passare a un altro pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b074-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="9b074-105">La deprecazione del pacchetto è diversa dall'annullamento dell' **elenco** del pacchetto, come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b074-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="9b074-106">L' **unlisting** di un pacchetto impedisce l'individuazione perché è nascosta nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="9b074-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="9b074-107">La **deprecazione** di un pacchetto consente ai consumer esistenti del pacchetto di scoprire se sono installati o usati nei progetti.</span><span class="sxs-lookup"><span data-stu-id="9b074-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="9b074-108">Consente inoltre di comprendere il motivo della deprecazione e un pacchetto alternativo consigliato come specificato dall'utente (editore del pacchetto).</span><span class="sxs-lookup"><span data-stu-id="9b074-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="9b074-109">La deprecazione di un pacchetto non comporta l'annullamento dell'elenco del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b074-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="9b074-110">Come server di pubblicazione, è possibile scegliere di non elencare i pacchetti e deprecarli.</span><span class="sxs-lookup"><span data-stu-id="9b074-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="9b074-111">Flusso di lavoro di deprecazione</span><span class="sxs-lookup"><span data-stu-id="9b074-111">Deprecation workflow</span></span>
1. <span data-ttu-id="9b074-112">Per deprecare un pacchetto, passare a **Gestisci pacchetti** e selezionare **deprecazione**:</span><span class="sxs-lookup"><span data-stu-id="9b074-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![Opzione Vai a deprecate Package](media/deprecation-select-option.png)

2. <span data-ttu-id="9b074-114">Selezionare la versione che si desidera deprecare.</span><span class="sxs-lookup"><span data-stu-id="9b074-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="9b074-115">Se si desidera deprecare tutte le versioni, scegliere l'opzione **Seleziona tutte le versioni** .</span><span class="sxs-lookup"><span data-stu-id="9b074-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![Selezionare le versioni del pacchetto da deprecare](media/deprecation-select-version.png)

3. <span data-ttu-id="9b074-117">Scegliere un motivo per la deprecazione.</span><span class="sxs-lookup"><span data-stu-id="9b074-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="9b074-118">Se il pacchetto non viene più mantenuto, scegliere l'opzione **legacy** .</span><span class="sxs-lookup"><span data-stu-id="9b074-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="9b074-119">Se la versione specifica presenta un bug critico, scegliere l'opzione **con i bug critici** .</span><span class="sxs-lookup"><span data-stu-id="9b074-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="9b074-120">Per qualsiasi altro motivo, selezionare **altro**.</span><span class="sxs-lookup"><span data-stu-id="9b074-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="9b074-121">È sempre possibile specificare un pacchetto (e una versione) consigliato alternativo e un messaggio personalizzato per i proprietari.</span><span class="sxs-lookup"><span data-stu-id="9b074-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![Select reasons alternative Package Recommendation e Custom Message](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="9b074-123">Il messaggio personalizzato viene visualizzato solo in nuget.org ma non dai client.</span><span class="sxs-lookup"><span data-stu-id="9b074-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="9b074-124">Attualmente, i client come `dotnet.exe` e gestione pacchetti NuGet non visualizzano il messaggio personalizzato.</span><span class="sxs-lookup"><span data-stu-id="9b074-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="9b074-125">Esperienza client per Pacchetti deprecati</span><span class="sxs-lookup"><span data-stu-id="9b074-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="9b074-126">Una volta che un pacchetto è stato deprecato, i relativi consumer riceveranno una notifica nei modi seguenti, a seconda del client usato.</span><span class="sxs-lookup"><span data-stu-id="9b074-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="9b074-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b074-127">Visual Studio</span></span> 
<span data-ttu-id="9b074-128">*Disponibile a partire da Visual Studio 2019 versione 16,3*</span><span class="sxs-lookup"><span data-stu-id="9b074-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="9b074-129">In Visual Studio viene visualizzato un avviso relativo all'utilizzo di un pacchetto `Installed` deprecato nella scheda. Verrà visualizzato il pacchetto e le relative informazioni di deprecazione (incluso il motivo per cui è stato deprecato e il pacchetto alternativo da usare, se presente).</span><span class="sxs-lookup"><span data-stu-id="9b074-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab.It will lead you to the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Pacchetti deprecati nella scheda installato di Visual Studio di gestione pacchetti](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="9b074-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="9b074-131">dotnet.exe</span></span>
<span data-ttu-id="9b074-132">*Disponibile a partire da .NET SDK 3,0*</span><span class="sxs-lookup"><span data-stu-id="9b074-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="9b074-133">Se si utilizza dotnet. exe, è possibile eseguire il comando `dotnet list package --deprecated` nella cartella della soluzione o del progetto per ottenere un elenco di Pacchetti deprecati insieme alle informazioni di deprecazione:</span><span class="sxs-lookup"><span data-stu-id="9b074-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
