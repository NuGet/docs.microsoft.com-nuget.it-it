---
title: Note sulla versione di NuGet 1,6
description: Note sulla versione per NuGet 1,6, inclusi problemi noti, correzioni di bug, funzionalità aggiunte e DCR.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777016"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="5fce5-103">Note sulla versione di NuGet 1,6</span><span class="sxs-lookup"><span data-stu-id="5fce5-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="5fce5-104">Note sulla versione di [NuGet 1,5](../release-notes/nuget-1.5.md)  |  [Note sulla versione di NuGet 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="5fce5-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="5fce5-105">NuGet 1,6 è stato rilasciato il 13 dicembre 2011.</span><span class="sxs-lookup"><span data-stu-id="5fce5-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="5fce5-106">Problema di installazione noto</span><span class="sxs-lookup"><span data-stu-id="5fce5-106">Known Installation Issue</span></span>
<span data-ttu-id="5fce5-107">Se si esegue VS 2010 SP1, potrebbe essere rilevato un errore di installazione quando si tenta di aggiornare NuGet se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="5fce5-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="5fce5-108">La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5fce5-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="5fce5-109">Per altre informazioni, vedere <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="5fce5-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="5fce5-110">Nota: se Visual Studio non consente di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), probabilmente è necessario riavviare Visual Studio usando "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="5fce5-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="5fce5-111">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="5fce5-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="5fce5-112">Supporto per i pacchetti di versioni non definitive e semantiche</span><span class="sxs-lookup"><span data-stu-id="5fce5-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="5fce5-113">NuGet 1,6 introduce il supporto per il controllo delle versioni semantico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="5fce5-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="5fce5-114">Per ulteriori informazioni sull'utilizzo di SemVer, vedere la [documentazione relativa al controllo delle versioni](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="5fce5-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="5fce5-115">Uso di NuGet senza archiviare i pacchetti (ripristino dei pacchetti)</span><span class="sxs-lookup"><span data-stu-id="5fce5-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="5fce5-116">NuGet 1,6 dispone ora del supporto di prima classe per il flusso di lavoro in cui i pacchetti NuGet non vengono aggiunti al controllo del codice sorgente, ma vengono ripristinati in fase di compilazione se mancanti.</span><span class="sxs-lookup"><span data-stu-id="5fce5-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="5fce5-117">Per altri dettagli, vedere l'argomento [uso di NuGet senza eseguire il commit dei pacchetti nel controllo del codice sorgente](../consume-packages/packages-and-source-control.md) .</span><span class="sxs-lookup"><span data-stu-id="5fce5-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="5fce5-118">Modelli di elemento che installano pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="5fce5-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="5fce5-119">Basandosi sul lavoro per supportare il pacchetto NuGet preinstallato nei modelli di progetto di Visual Studio, NuGet 1,6 aggiunge anche il supporto per i modelli di elemento di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5fce5-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="5fce5-120">Ai modelli di elemento possono essere associati pacchetti NuGet installati quando il modello viene richiamato.</span><span class="sxs-lookup"><span data-stu-id="5fce5-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="5fce5-121">Per altri dettagli su come modificare un modello di progetto o di elemento per installare i pacchetti NuGet, vedere l'argomento [pacchetti in modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="5fce5-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="5fce5-122">Supporto per la disabilitazione delle origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="5fce5-122">Support for disabling package sources</span></span>
<span data-ttu-id="5fce5-123">Quando vengono configurate più origini di pacchetti, NuGet cercherà i pacchetti durante l'installazione di un pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="5fce5-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="5fce5-124">Un'origine del pacchetto inattiva per qualche motivo può rallentare gravemente NuGet.</span><span class="sxs-lookup"><span data-stu-id="5fce5-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="5fce5-125">Prima di NuGet 1,6, era possibile rimuovere l'origine del pacchetto, ma è necessario ricordare i dettagli relativi al momento in cui si vuole aggiungerlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="5fce5-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="5fce5-126">NuGet 1,6 consente di deselezionare un'origine del pacchetto per disabilitarla, ma è possibile mantenerla.</span><span class="sxs-lookup"><span data-stu-id="5fce5-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Disabilitazione di un pacchetto](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="5fce5-128">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="5fce5-128">Bug Fixes</span></span>
<span data-ttu-id="5fce5-129">NuGet 1,6 aveva un totale di 106 elementi di lavoro corretti.</span><span class="sxs-lookup"><span data-stu-id="5fce5-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="5fce5-130">95 di questi elementi sono stati classificati come bug e 10 di questi sono funzionalità.</span><span class="sxs-lookup"><span data-stu-id="5fce5-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="5fce5-131">Per un elenco completo degli elementi di lavoro corretti in NuGet 1,6, vedere la pagina [relativa al rilevamento dei problemi di NuGet per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="5fce5-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
