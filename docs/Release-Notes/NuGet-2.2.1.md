---
title: Note sulla versione 2.2.1 NuGet | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 39ceaeb3-2d33-4b1c-b195-eba36c6cbf9a
description: "Note sulla versione per l'inclusione di NuGet 2.2.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.2.1 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c31150572b4b6e066643ebcf0d92be16b25c6e19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="688a1-104">Note sulla versione 2.2.1 NuGet</span><span class="sxs-lookup"><span data-stu-id="688a1-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="688a1-105">[Note sulla versione 2.2 NuGet](../release-notes/nuget-2.2.md) | [note sulla versione di NuGet 2.5](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="688a1-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="688a1-106">È stata rilasciata NuGet 2.2.1 15 febbraio 2013.</span><span class="sxs-lookup"><span data-stu-id="688a1-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="688a1-107">Il numero di versione di estensione di Visual Studio è 2.2.40116.9051.</span><span class="sxs-lookup"><span data-stu-id="688a1-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="688a1-108">Aggiornamento di localizzazione</span><span class="sxs-lookup"><span data-stu-id="688a1-108">Localization Refresh</span></span>
<span data-ttu-id="688a1-109">NuGet fornito come parte di Visual Studio 2012, è stato completamente localizzato in inglese + 13 altri linguaggi.</span><span class="sxs-lookup"><span data-stu-id="688a1-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="688a1-110">Da allora NuGet 2.1 e 2.2 spediti ma la localizzazione non è stata aggiornata.</span><span class="sxs-lookup"><span data-stu-id="688a1-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="688a1-111">La versione NuGet 2.2.1 aggiorna la localizzazione.</span><span class="sxs-lookup"><span data-stu-id="688a1-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="688a1-112">Interfaccia utente e la Console di PowerShell di NuGet sono localizzati nelle lingue seguenti:</span><span class="sxs-lookup"><span data-stu-id="688a1-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="688a1-113">Cinese (semplificato)</span><span class="sxs-lookup"><span data-stu-id="688a1-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="688a1-114">Cinese (tradizionale)</span><span class="sxs-lookup"><span data-stu-id="688a1-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="688a1-115">Ceco</span><span class="sxs-lookup"><span data-stu-id="688a1-115">Czech</span></span>
1. <span data-ttu-id="688a1-116">Inglese</span><span class="sxs-lookup"><span data-stu-id="688a1-116">English</span></span>
1. <span data-ttu-id="688a1-117">Francese</span><span class="sxs-lookup"><span data-stu-id="688a1-117">French</span></span>
1. <span data-ttu-id="688a1-118">Tedesco</span><span class="sxs-lookup"><span data-stu-id="688a1-118">German</span></span>
1. <span data-ttu-id="688a1-119">Italiano</span><span class="sxs-lookup"><span data-stu-id="688a1-119">Italian</span></span>
1. <span data-ttu-id="688a1-120">Giapponese</span><span class="sxs-lookup"><span data-stu-id="688a1-120">Japanese</span></span>
1. <span data-ttu-id="688a1-121">Coreano</span><span class="sxs-lookup"><span data-stu-id="688a1-121">Korean</span></span>
1. <span data-ttu-id="688a1-122">Polacco</span><span class="sxs-lookup"><span data-stu-id="688a1-122">Polish</span></span>
1. <span data-ttu-id="688a1-123">Portoghese (Brasile)</span><span class="sxs-lookup"><span data-stu-id="688a1-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="688a1-124">Russo</span><span class="sxs-lookup"><span data-stu-id="688a1-124">Russian</span></span>
1. <span data-ttu-id="688a1-125">Spagnolo</span><span class="sxs-lookup"><span data-stu-id="688a1-125">Spanish</span></span>
1. <span data-ttu-id="688a1-126">Turco</span><span class="sxs-lookup"><span data-stu-id="688a1-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="688a1-127">Modelli di Visual Studio supportano più repository di pacchetti preinstallati</span><span class="sxs-lookup"><span data-stu-id="688a1-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="688a1-128">Se si producono modelli di Visual Studio, è possibile utilizzare NuGet per [preinstallare pacchetti](../visual-studio-extensibility/visual-studio-templates.md) come parte del modello.</span><span class="sxs-lookup"><span data-stu-id="688a1-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="688a1-129">Fino ad ora, questa funzionalità era una limitazione che tutti i pacchetti necessari per provenire dalla stessa origine.</span><span class="sxs-lookup"><span data-stu-id="688a1-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="688a1-130">Con NuGet 2.2.1, tuttavia, è possibile disporre di pacchetti installati in più repository (all'interno del modello, un progetto VSIX o una cartella sul disco definito nel Registro di sistema).</span><span class="sxs-lookup"><span data-stu-id="688a1-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="688a1-131">Lo scenario principale per questa funzionalità è modelli di progetto ASP.NET personalizzati.</span><span class="sxs-lookup"><span data-stu-id="688a1-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="688a1-132">I modelli ASP.NET incorporati utilizzano pacchetti preinstallati, estrarre i pacchetti da disco locale.</span><span class="sxs-lookup"><span data-stu-id="688a1-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="688a1-133">È ora possibile creare un modello di progetto ASP.NET personalizzato che utilizza i pacchetti esistenti installati da ASP.NET, ma aggiungere pacchetti NuGet aggiuntivi nel modello.</span><span class="sxs-lookup"><span data-stu-id="688a1-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="688a1-134">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="688a1-134">Bug Fixes</span></span>
<span data-ttu-id="688a1-135">NuGet 2.2.1 include alcune correzioni di bug di destinazione.</span><span class="sxs-lookup"><span data-stu-id="688a1-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="688a1-136">Per un elenco di lavoro gli elementi corretti in NuGet 2.2.1,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="688a1-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="688a1-137">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="688a1-137">Known Issues</span></span>

<span data-ttu-id="688a1-138">Se si estende i modelli di progetto ASP.NET, tutti i repository di pacchetti preinstallati devono utilizzare lo stesso valore per il `isPreunzipped` attributo.</span><span class="sxs-lookup"><span data-stu-id="688a1-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
