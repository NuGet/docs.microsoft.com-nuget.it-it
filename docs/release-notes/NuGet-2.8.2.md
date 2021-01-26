---
title: Note sulla versione di NuGet 2.8.2
description: Note sulla versione per NuGet 2.8.2, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780364"
---
# <a name="nuget-282-release-notes"></a><span data-ttu-id="e630e-103">Note sulla versione di NuGet 2.8.2</span><span class="sxs-lookup"><span data-stu-id="e630e-103">NuGet 2.8.2 Release Notes</span></span>

<span data-ttu-id="e630e-104">Note sulla versione di [NuGet 2.8.1](../release-notes/nuget-2.8.1.md)  |  [Note sulla versione di NuGet 2.8.3](../release-notes/nuget-2.8.3.md)</span><span class="sxs-lookup"><span data-stu-id="e630e-104">[NuGet 2.8.1 Release Notes](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md)</span></span>

<span data-ttu-id="e630e-105">NuGet 2.8.2 è stato rilasciato il 22 maggio 2014.</span><span class="sxs-lookup"><span data-stu-id="e630e-105">NuGet 2.8.2 was released on May 22, 2014.</span></span>  <span data-ttu-id="e630e-106">Questa versione include solo le modifiche apportate al nuget.exe riga di comando, al pacchetto NuGet. Server e ad altri pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="e630e-106">This release only included changes to the nuget.exe command-line, the NuGet.Server package and other NuGet packages.</span></span>  <span data-ttu-id="e630e-107">La versione non include un'estensione di Visual Studio aggiornata o un'estensione di WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="e630e-107">The release did not include an updated Visual Studio extension or WebMatrix extension.</span></span>

## <a name="notable-updates"></a><span data-ttu-id="e630e-108">Aggiornamenti rilevanti</span><span class="sxs-lookup"><span data-stu-id="e630e-108">Notable Updates</span></span>

<span data-ttu-id="e630e-109">Gli aggiornamenti più significativi sono stati inclusi nella nuget.exe riga di comando e nel pacchetto NuGet. Server (per i feed NuGet indipendenti).</span><span class="sxs-lookup"><span data-stu-id="e630e-109">The most notable updates were in the nuget.exe command-line and the NuGet.Server package (for self-hosted NuGet feeds).</span></span>

### <a name="important-nugetexe-bug-fixes"></a><span data-ttu-id="e630e-110">Correzioni di bug importanti nuget.exe</span><span class="sxs-lookup"><span data-stu-id="e630e-110">Important nuget.exe Bug Fixes</span></span>

1. [<span data-ttu-id="e630e-111">nuget.exe push ha esito negativo e continua a riprovare</span><span class="sxs-lookup"><span data-stu-id="e630e-111">nuget.exe Push fails and keeps retrying</span></span>](https://nuget.codeplex.com/workitem/4000)
1. [<span data-ttu-id="e630e-112">nuget.exe push non invia correttamente le credenziali di autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="e630e-112">nuget.exe Push does not send Basic Auth credentials correctly</span></span>](https://nuget.codeplex.com/workitem/4109)
1. [<span data-ttu-id="e630e-113">nuget.exe push non segue il reindirizzamento temporaneo</span><span class="sxs-lookup"><span data-stu-id="e630e-113">nuget.exe Push won't follow temporary redirect</span></span>](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a><span data-ttu-id="e630e-114">Correzione di bug NuGet. Server importante</span><span class="sxs-lookup"><span data-stu-id="e630e-114">Important NuGet.Server Bug Fix</span></span>

1. [<span data-ttu-id="e630e-115">Il valore di IsAbsoluteLatestVersion restituito da NuGet. Server non è corretto</span><span class="sxs-lookup"><span data-stu-id="e630e-115">Wrong value of IsAbsoluteLatestVersion returned by NuGet.Server</span></span>](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a><span data-ttu-id="e630e-116">Pacchetti aggiornati</span><span class="sxs-lookup"><span data-stu-id="e630e-116">Packages Updated</span></span>

<span data-ttu-id="e630e-117">Le correzioni della riga di comando nuget.exe e NuGet. Server vengono fornite come aggiornamenti dei pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="e630e-117">The nuget.exe command-line and NuGet.Server fixes are shipped as NuGet package updates.</span></span>  <span data-ttu-id="e630e-118">Sono stati aggiornati anche altri pacchetti con 2.8.2.</span><span class="sxs-lookup"><span data-stu-id="e630e-118">There were other packages updated with 2.8.2 as well.</span></span>

<span data-ttu-id="e630e-119">Ecco l'elenco dei pacchetti aggiornati:</span><span class="sxs-lookup"><span data-stu-id="e630e-119">Here's the list of updated packages:</span></span>

1. [<span data-ttu-id="e630e-120">NuGet. Core</span><span class="sxs-lookup"><span data-stu-id="e630e-120">NuGet.Core</span></span>](https://www.nuget.org/packages/NuGet.Core/)
1. [<span data-ttu-id="e630e-121">NuGet. CommandLine</span><span class="sxs-lookup"><span data-stu-id="e630e-121">NuGet.CommandLine</span></span>](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [<span data-ttu-id="e630e-122">NuGet.Server</span><span class="sxs-lookup"><span data-stu-id="e630e-122">NuGet.Server</span></span>](https://www.nuget.org/packages/NuGet.Server/)
1. [<span data-ttu-id="e630e-123">NuGet. Build</span><span class="sxs-lookup"><span data-stu-id="e630e-123">NuGet.Build</span></span>](https://www.nuget.org/packages/NuGet.Build/)
1. <span data-ttu-id="e630e-124">[NuGet. VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (pacchetto, non estensione)</span><span class="sxs-lookup"><span data-stu-id="e630e-124">[NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (the package, not the extension)</span></span>

## <a name="all-changes"></a><span data-ttu-id="e630e-125">Tutte le modifiche</span><span class="sxs-lookup"><span data-stu-id="e630e-125">All Changes</span></span>
<span data-ttu-id="e630e-126">Sono stati risolti 10 problemi nella versione.</span><span class="sxs-lookup"><span data-stu-id="e630e-126">There were 10 issues addressed in the release.</span></span> <span data-ttu-id="e630e-127">Per un elenco completo degli elementi di lavoro corretti in NuGet 2.8.2, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="e630e-127">For a full list of the work items fixed in NuGet 2.8.2, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>
