---
title: Note sulla versione di NuGet 2.8.2 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: bb547f5d-3c0e-4721-b2c7-3fc7e09c34de
description: "Note sulla versione per l'inclusione di NuGet 2.8.2 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.2 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 221b8970663ca80a986fc3ee542b99971c5e2018
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="3af99-104">Note sulla versione di NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="3af99-104">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="3af99-105">[Note sulla versione di NuGet 2.8.1](../release-notes/nuget-2.8.1.md) | [note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="3af99-105">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="3af99-106">NuGet 2.8.2 è stato rilasciato il 22 maggio 2014.</span><span class="sxs-lookup"><span data-stu-id="3af99-106">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="3af99-107">Questa versione è incluso solo le modifiche per la riga di comando di nuget.exe, il pacchetto NuGet.Server e altri pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="3af99-107">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="3af99-108">La versione non include un'estensione aggiornata di Visual Studio o estensione di WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="3af99-108">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="3af99-109">Aggiornamenti importanti</span><span class="sxs-lookup"><span data-stu-id="3af99-109">Notable Updates</span></span>

<span data-ttu-id="3af99-110">Gli aggiornamenti più importanti siano stati di nuget.exe della riga di comando e il pacchetto NuGet.Server (per i feed NuGet indipendente).</span><span class="sxs-lookup"><span data-stu-id="3af99-110">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="3af99-111">Correzioni di Bug importanti nuget.exe</span><span class="sxs-lookup"><span data-stu-id="3af99-111">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="3af99-112">NuGet.exe Push ha esito negativo e mantiene nuovo tentativo in corso</span><span class="sxs-lookup"><span data-stu-id="3af99-112">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="3af99-113">NuGet.exe Push non invia correttamente le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="3af99-113">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="3af99-114">NuGet.exe Push non seguire reindirizzamento temporaneo</span><span class="sxs-lookup"><span data-stu-id="3af99-114">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="3af99-115">Correzione di Bug importanti NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3af99-115">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="3af99-116">Valore non corretto di IsAbsoluteLatestVersion restituito da NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3af99-116">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="3af99-117">Pacchetti aggiornati</span><span class="sxs-lookup"><span data-stu-id="3af99-117">Packages Updated</span></span>

<span data-ttu-id="3af99-118">Le nuget.exe della riga di comando e le correzioni NuGet.Server vengono fornite come aggiornamenti pacchetto NuGet.</span><span class="sxs-lookup"><span data-stu-id="3af99-118">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="3af99-119">Si sono verificati altri pacchetti aggiornati con 2.8.2 anche.</span><span class="sxs-lookup"><span data-stu-id="3af99-119">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="3af99-120">Di seguito è riportato l'elenco dei pacchetti aggiornati:</span><span class="sxs-lookup"><span data-stu-id="3af99-120">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="3af99-121">Sono</span><span class="sxs-lookup"><span data-stu-id="3af99-121">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="3af99-122">NuGet.CommandLine</span><span class="sxs-lookup"><span data-stu-id="3af99-122">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="3af99-123">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="3af99-123">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="3af99-124">NuGet.Build</span><span class="sxs-lookup"><span data-stu-id="3af99-124">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="3af99-125">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (il pacchetto, non l'estensione)</span><span class="sxs-lookup"><span data-stu-id="3af99-125">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="3af99-126">Tutte le modifiche</span><span class="sxs-lookup"><span data-stu-id="3af99-126">All Changes</span></span>
<span data-ttu-id="3af99-127">Si sono verificati i 10 problemi risolti nella versione.</span><span class="sxs-lookup"><span data-stu-id="3af99-127">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="3af99-128">Per un elenco completo delle operazioni gli elementi corretti in NuGet, 2.8.2 visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="3af99-128">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
