---
title: Note sulla versione di NuGet 2.8.1
description: Note sulla versione per NuGet 2.8.1, tra cui noti problemi, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545239"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="efd49-103">Note sulla versione di NuGet 2.8.1</span><span class="sxs-lookup"><span data-stu-id="efd49-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="efd49-104">[Note sulla versione di NuGet 2.8](../release-notes/nuget-2.8.md) | [note sulla versione di NuGet 2.8.2](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="efd49-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="efd49-105">NuGet 2.8.1 è stato rilasciato dal 2 aprile 2014.</span><span class="sxs-lookup"><span data-stu-id="efd49-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="efd49-106">Funzionalità di rilievo nella versione</span><span class="sxs-lookup"><span data-stu-id="efd49-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="efd49-107">Supporto per i progetti di Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="efd49-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="efd49-108">Questa versione supporta ora il seguente nuovo target framework moniker che può essere utilizzato per i progetti di destinazione Windows Phone 8.1:</span><span class="sxs-lookup"><span data-stu-id="efd49-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="efd49-109">WindowsPhone81 / WP81 (per i progetti Windows Phone basate su Silverlight)</span><span class="sxs-lookup"><span data-stu-id="efd49-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="efd49-110">WindowsPhoneApp81 / WPA81 (per i progetti di App di Windows Phone basate su WinRT)</span><span class="sxs-lookup"><span data-stu-id="efd49-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="efd49-111">Aggiornamento dell'estensione di WebMatrix NuGet</span><span class="sxs-lookup"><span data-stu-id="efd49-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="efd49-112">Questa versione aggiorna il client di NuGet in WebMatrix per trovare [togliere](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 e offre con include, ad esempio le trasformazioni XDT.</span><span class="sxs-lookup"><span data-stu-id="efd49-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="efd49-113">Ancora più importante, la versione 2.6.1 update core consente al client di WebMatrix installare i pacchetti NuGet che contengono le versioni più recenti del `.nuspec` schema, che include i pacchetti NuGet ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="efd49-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="efd49-114">Per altre informazioni sull'aggiornamento dell'estensione di WebMatrix, vedere quelli specifici [note sulla versione](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span><span class="sxs-lookup"><span data-stu-id="efd49-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="efd49-115">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="efd49-115">Bug Fixes</span></span>
<span data-ttu-id="efd49-116">Oltre a queste funzionalità, questa versione di NuGet include altre correzioni di bug.</span><span class="sxs-lookup"><span data-stu-id="efd49-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="efd49-117">Si sono verificati problemi totali 16 risolti nella versione.</span><span class="sxs-lookup"><span data-stu-id="efd49-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="efd49-118">Per un elenco completo delle operazioni elementi risolti in NuGet 2.8.1, vista la [NuGet Issue Tracker per questa versione](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span><span class="sxs-lookup"><span data-stu-id="efd49-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="efd49-119">Aggregano con Visual Studio "14" CTP</span><span class="sxs-lookup"><span data-stu-id="efd49-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="efd49-120">Nella versione CTP di Visual Studio "14" rilasciata nel mese di giugno 2014 3rd NuGet 2.8.1 viene fornito nella casella.</span><span class="sxs-lookup"><span data-stu-id="efd49-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="efd49-121">Le funzionalità supportano restano in par con altri 2.8.1 VSIXes come quello per Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="efd49-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
