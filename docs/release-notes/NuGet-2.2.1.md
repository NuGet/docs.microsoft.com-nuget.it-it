---
title: Note sulla versione di NuGet 2.2.1
description: Note sulla versione per NuGet 2.2.1 inclusi noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550698"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="bb8ec-103">Note sulla versione di NuGet 2.2.1</span><span class="sxs-lookup"><span data-stu-id="bb8ec-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="bb8ec-104">[Note sulla versione di NuGet 2.2](../release-notes/nuget-2.2.md) | [note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="bb8ec-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="bb8ec-105">NuGet 2.2.1 è stato rilasciato il 15 febbraio 2013.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="bb8ec-106">Il numero di versione di estensione di Visual Studio è 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="bb8ec-107">Aggiornamento localizzazione</span><span class="sxs-lookup"><span data-stu-id="bb8ec-107">Localization Refresh</span></span>
<span data-ttu-id="bb8ec-108">Quando NuGet fornito come parte di Visual Studio 2012, si è stato completamente localizzato nelle inglese + 13 altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="bb8ec-109">Da allora, sono spedite NuGet 2.1 e 2.2, ma la localizzazione non era stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="bb8ec-110">La versione per NuGet 2.2.1 aggiorna la localizzazione.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="bb8ec-111">Interfaccia utente e la Console di PowerShell di NuGet sono localizzati nelle lingue seguenti:</span><span class="sxs-lookup"><span data-stu-id="bb8ec-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="bb8ec-112">Cinese (semplificato)</span><span class="sxs-lookup"><span data-stu-id="bb8ec-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="bb8ec-113">Cinese (tradizionale)</span><span class="sxs-lookup"><span data-stu-id="bb8ec-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="bb8ec-114">Ceco</span><span class="sxs-lookup"><span data-stu-id="bb8ec-114">Czech</span></span>
1. <span data-ttu-id="bb8ec-115">Inglese</span><span class="sxs-lookup"><span data-stu-id="bb8ec-115">English</span></span>
1. <span data-ttu-id="bb8ec-116">Francese</span><span class="sxs-lookup"><span data-stu-id="bb8ec-116">French</span></span>
1. <span data-ttu-id="bb8ec-117">Tedesco</span><span class="sxs-lookup"><span data-stu-id="bb8ec-117">German</span></span>
1. <span data-ttu-id="bb8ec-118">Italiano</span><span class="sxs-lookup"><span data-stu-id="bb8ec-118">Italian</span></span>
1. <span data-ttu-id="bb8ec-119">Giapponese</span><span class="sxs-lookup"><span data-stu-id="bb8ec-119">Japanese</span></span>
1. <span data-ttu-id="bb8ec-120">Coreano</span><span class="sxs-lookup"><span data-stu-id="bb8ec-120">Korean</span></span>
1. <span data-ttu-id="bb8ec-121">Polacco</span><span class="sxs-lookup"><span data-stu-id="bb8ec-121">Polish</span></span>
1. <span data-ttu-id="bb8ec-122">Portoghese (Brasile)</span><span class="sxs-lookup"><span data-stu-id="bb8ec-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="bb8ec-123">Russo</span><span class="sxs-lookup"><span data-stu-id="bb8ec-123">Russian</span></span>
1. <span data-ttu-id="bb8ec-124">Spagnolo</span><span class="sxs-lookup"><span data-stu-id="bb8ec-124">Spanish</span></span>
1. <span data-ttu-id="bb8ec-125">Turco</span><span class="sxs-lookup"><span data-stu-id="bb8ec-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="bb8ec-126">Modelli di Visual Studio supportano più i repository dei pacchetti preinstallati</span><span class="sxs-lookup"><span data-stu-id="bb8ec-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="bb8ec-127">Se si producono modelli di Visual Studio, è possibile usare NuGet per [preinstallare pacchetti](../visual-studio-extensibility/visual-studio-templates.md) come parte del modello.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="bb8ec-128">Fino ad ora, questa funzionalità era una limitazione che tutti i pacchetti necessari per provengono dalla stessa origine.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="bb8ec-129">Con NuGet 2.2.1 però, è possibile avere i pacchetti installati da più repository (all'interno del modello, un progetto VSIX o una cartella sul disco definito nel Registro di sistema).</span><span class="sxs-lookup"><span data-stu-id="bb8ec-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="bb8ec-130">Lo scenario principale per questa funzionalità è i modelli di progetto personalizzati di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="bb8ec-131">I modelli predefiniti di ASP.NET usano pacchetti preinstallati, estraggano pacchetti dal disco locale.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="bb8ec-132">È ora possibile creare un modello di progetto ASP.NET personalizzato che usa i pacchetti esistenti installati da ASP.NET ma aggiungere pacchetti NuGet aggiuntivi al modello.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="bb8ec-133">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="bb8ec-133">Bug Fixes</span></span>
<span data-ttu-id="bb8ec-134">NuGet 2.2.1 include alcune correzioni di bug di destinazione.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="bb8ec-135">Per un elenco di lavoro elementi di risolti in NuGet 2.2.1, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="bb8ec-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="bb8ec-136">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="bb8ec-136">Known Issues</span></span>

<span data-ttu-id="bb8ec-137">Se si intende estendere i modelli di progetto ASP.NET, tutti i repository dei pacchetti preinstallati devono usare lo stesso valore per il `isPreunzipped` attributo.</span><span class="sxs-lookup"><span data-stu-id="bb8ec-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
