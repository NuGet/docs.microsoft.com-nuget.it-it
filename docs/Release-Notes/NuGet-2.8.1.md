---
title: Note sulla versione di NuGet 2.8.1 | Documenti Microsoft
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: eebbbae4-fc6a-4c05-9102-4ec66b4c64a4
description: "Note sulla versione per l'inclusione di NuGet 2.8.1 problemi noti, correzioni di bug, le funzionalità aggiunte e dcr."
keywords: "NuGet 2.8.1 note sulla versione, correzioni di bug, problemi noti, aggiunta di funzionalità, eseguire"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ac33369644d312591bfe8c06540935b2c6063c5d
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="f76f1-104">Note sulla versione di NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="f76f1-104">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="f76f1-105">[Note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 note](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="f76f1-105">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="f76f1-106">È stata rilasciata NuGet 2.8.1 2 aprile 2014.</span><span class="sxs-lookup"><span data-stu-id="f76f1-106">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="f76f1-107">Importanti funzionalità nella versione</span><span class="sxs-lookup"><span data-stu-id="f76f1-107">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="f76f1-108">Supporto per i progetti Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="f76f1-108">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="f76f1-109">Questa versione supporta ora i moniker seguente nuovo framework di destinazione che possono essere utilizzato per i progetti di destinazione Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="f76f1-109">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="f76f1-110">WindowsPhone81 / WP81 (per i progetti di Windows Phone basate su Silverlight)</span><span class="sxs-lookup"><span data-stu-id="f76f1-110">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="f76f1-111">WindowsPhoneApp81 / WPA81 (per i progetti di App di Windows Phone basate su WinRT)</span><span class="sxs-lookup"><span data-stu-id="f76f1-111">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="f76f1-112">Aggiornamento dell'estensione di WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="f76f1-112">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="f76f1-113">Questa versione aggiorna il client NuGet trovato in WebMatrix per [sono](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e la porta con comprende, ad esempio trasformazioni XDT.</span><span class="sxs-lookup"><span data-stu-id="f76f1-113">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="f76f1-114">Ancora più importante, la 2.6.1 aggiornamento core consente al client di WebMatrix installare i pacchetti NuGet che contengono le versioni più recenti del `.nuspec` schema, che include i pacchetti NuGet di ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f76f1-114">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="f76f1-115">Per ulteriori informazioni sull'aggiornamento dell'estensione di WebMatrix, vedere parametri specifici [note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="f76f1-115">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="f76f1-116">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="f76f1-116">Bug Fixes</span></span>
<span data-ttu-id="f76f1-117">Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="f76f1-117">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="f76f1-118">Si sono verificati problemi di totali 16 risolti nella versione.</span><span class="sxs-lookup"><span data-stu-id="f76f1-118">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="f76f1-119">Per un elenco completo delle operazioni gli elementi corretti in NuGet, 2.8.1 visualizzazione di [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="f76f1-119">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="f76f1-120">Reshipping con Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="f76f1-120">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="f76f1-121">Nella versione CTP di Visual Studio "14" rilasciata a giugno 2014 3rd NuGet 2.8.1 viene fornito nella casella.</span><span class="sxs-lookup"><span data-stu-id="f76f1-121">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="f76f1-122">Le funzionalità supportano restano in pari con altri 2.8.1 VSIXes ad esempio quello per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f76f1-122">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
