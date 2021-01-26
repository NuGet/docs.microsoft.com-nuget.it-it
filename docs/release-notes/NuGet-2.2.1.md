---
title: Note sulla versione di NuGet 2.2.1
description: Note sulla versione per NuGet 2.2.1, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776813"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="97c45-103">Note sulla versione di NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="97c45-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="97c45-104">Note sulla versione di [NuGet 2,2](../release-notes/nuget-2.2.md)  |  [Note sulla versione di NuGet 2,5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="97c45-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="97c45-105">NuGet 2.2.1 è stato rilasciato il 15 febbraio 2013.</span><span class="sxs-lookup"><span data-stu-id="97c45-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="97c45-106">Il numero di versione dell'estensione di Visual Studio è 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="97c45-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="97c45-107">Aggiornamento della localizzazione</span><span class="sxs-lookup"><span data-stu-id="97c45-107">Localization Refresh</span></span>
<span data-ttu-id="97c45-108">Quando NuGet è stato fornito come parte di Visual Studio 2012, è stato completamente localizzato in inglese + 13 altre lingue.</span><span class="sxs-lookup"><span data-stu-id="97c45-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="97c45-109">Da allora, NuGet 2,1 e 2,2 sono stati spediti ma la localizzazione non è stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="97c45-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="97c45-110">La versione di NuGet 2.2.1 Aggiorna la localizzazione.</span><span class="sxs-lookup"><span data-stu-id="97c45-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="97c45-111">L'interfaccia utente e la console di PowerShell di NuGet sono localizzate nelle seguenti lingue:</span><span class="sxs-lookup"><span data-stu-id="97c45-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="97c45-112">Cinese (semplificato)</span><span class="sxs-lookup"><span data-stu-id="97c45-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="97c45-113">Cinese (tradizionale)</span><span class="sxs-lookup"><span data-stu-id="97c45-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="97c45-114">Ceco</span><span class="sxs-lookup"><span data-stu-id="97c45-114">Czech</span></span>
1. <span data-ttu-id="97c45-115">Inglese</span><span class="sxs-lookup"><span data-stu-id="97c45-115">English</span></span>
1. <span data-ttu-id="97c45-116">Francese</span><span class="sxs-lookup"><span data-stu-id="97c45-116">French</span></span>
1. <span data-ttu-id="97c45-117">Tedesco</span><span class="sxs-lookup"><span data-stu-id="97c45-117">German</span></span>
1. <span data-ttu-id="97c45-118">Italiano</span><span class="sxs-lookup"><span data-stu-id="97c45-118">Italian</span></span>
1. <span data-ttu-id="97c45-119">Giapponese</span><span class="sxs-lookup"><span data-stu-id="97c45-119">Japanese</span></span>
1. <span data-ttu-id="97c45-120">Coreano</span><span class="sxs-lookup"><span data-stu-id="97c45-120">Korean</span></span>
1. <span data-ttu-id="97c45-121">Polacco</span><span class="sxs-lookup"><span data-stu-id="97c45-121">Polish</span></span>
1. <span data-ttu-id="97c45-122">Portoghese (Brasile)</span><span class="sxs-lookup"><span data-stu-id="97c45-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="97c45-123">Russo</span><span class="sxs-lookup"><span data-stu-id="97c45-123">Russian</span></span>
1. <span data-ttu-id="97c45-124">Spagnolo</span><span class="sxs-lookup"><span data-stu-id="97c45-124">Spanish</span></span>
1. <span data-ttu-id="97c45-125">Turco</span><span class="sxs-lookup"><span data-stu-id="97c45-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="97c45-126">I modelli di Visual Studio supportano più repository di pacchetti preinstallati</span><span class="sxs-lookup"><span data-stu-id="97c45-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="97c45-127">Se si producono modelli di Visual Studio, è possibile usare NuGet per [preinstallare i pacchetti](../visual-studio-extensibility/visual-studio-templates.md) come parte del modello.</span><span class="sxs-lookup"><span data-stu-id="97c45-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="97c45-128">Fino ad ora, questa funzionalità aveva una limitazione che tutti i pacchetti dovevano provenire dalla stessa origine.</span><span class="sxs-lookup"><span data-stu-id="97c45-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="97c45-129">Con NuGet 2.2.1, tuttavia, i pacchetti possono essere installati da più repository, all'interno del modello, in un progetto VSIX o in una cartella su disco definita nel registro di sistema.</span><span class="sxs-lookup"><span data-stu-id="97c45-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="97c45-130">Lo scenario principale di questa funzionalità è il modello di progetto ASP.NET personalizzato.</span><span class="sxs-lookup"><span data-stu-id="97c45-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="97c45-131">I modelli ASP.NET predefiniti usano i pacchetti preinstallati, estraendo i pacchetti dal disco locale.</span><span class="sxs-lookup"><span data-stu-id="97c45-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="97c45-132">È ora possibile creare un modello di progetto ASP.NET personalizzato che usa i pacchetti esistenti installati da ASP.NET ma aggiungere pacchetti NuGet aggiuntivi al modello.</span><span class="sxs-lookup"><span data-stu-id="97c45-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="97c45-133">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="97c45-133">Bug Fixes</span></span>
<span data-ttu-id="97c45-134">NuGet 2.2.1 include alcune correzioni di bug mirate.</span><span class="sxs-lookup"><span data-stu-id="97c45-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="97c45-135">Per un elenco degli elementi di lavoro corretti in NuGet 2.2.1, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="97c45-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="97c45-136">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="97c45-136">Known Issues</span></span>

<span data-ttu-id="97c45-137">Se si estendono i modelli di progetto ASP.NET, tutti i repository di pacchetti preinstallati devono usare lo stesso valore per l' `isPreunzipped` attributo.</span><span class="sxs-lookup"><span data-stu-id="97c45-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
