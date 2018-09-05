---
title: Note sulla versione 1.6 di NuGet
description: Note sulla versione per NuGet 1.6 inclusi i problemi noti, correzioni di bug, funzionalità aggiunte e dcr.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549012"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="67220-103">Note sulla versione 1.6 di NuGet</span><span class="sxs-lookup"><span data-stu-id="67220-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="67220-104">[Note sulla versione di NuGet 1.5](../release-notes/nuget-1.5.md) | [note sulla versione di NuGet 1.7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="67220-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="67220-105">NuGet 1.6 è stato rilasciato il 13 dicembre 2011.</span><span class="sxs-lookup"><span data-stu-id="67220-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="67220-106">Problema di installazione noti</span><span class="sxs-lookup"><span data-stu-id="67220-106">Known Installation Issue</span></span>
<span data-ttu-id="67220-107">Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="67220-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="67220-108">Per risolvere il problema è sufficiente disinstallare NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67220-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="67220-109">Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="67220-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="67220-110">Nota: Se Visual Studio non consentirà di disinstallare l'estensione (il pulsante Disinstalla è disabilitato), quindi probabile che sia necessario riavviare Visual Studio tramite "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="67220-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="67220-111">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="67220-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="67220-112">Supporto per Versionamento semantico e i pacchetti di versione non definitivo</span><span class="sxs-lookup"><span data-stu-id="67220-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="67220-113">NuGet 1.6 introduce il supporto per Versionamento semantico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="67220-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="67220-114">Per altre informazioni su come viene utilizzato SemVer, leggere il [documentazione di controllo delle versioni](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="67220-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="67220-115">Usare NuGet senza il controllo nei pacchetti (ripristino dei pacchetti)</span><span class="sxs-lookup"><span data-stu-id="67220-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="67220-116">NuGet 1.6 ha ora supporto avanzato per il flusso di lavoro in cui NuGet pacchetti non vengono aggiunti al controllo del codice sorgente, ma invece vengono ripristinati in fase di compilazione se mancante.</span><span class="sxs-lookup"><span data-stu-id="67220-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="67220-117">Per altre informazioni, vedere la [tramite NuGet senza eseguire il commit di pacchetti al controllo del codice sorgente](../consume-packages/packages-and-source-control.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="67220-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="67220-118">Modelli di elemento di installazione dei pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="67220-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="67220-119">Compila il lavoro per supportare i pacchetti NuGet preinstallati ai modelli di progetto di Visual Studio, NuGet 1.6 aggiunge anche il supporto per i modelli di elemento di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67220-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="67220-120">È possibile associare i pacchetti NuGet vengono installati quando viene richiamato il modello in modelli di elemento.</span><span class="sxs-lookup"><span data-stu-id="67220-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="67220-121">Per altre informazioni su come modificare un modello di progetto/elemento per installare i pacchetti NuGet, vedere la [pacchetti di modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="67220-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="67220-122">Supporto per la disabilitazione di origini dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="67220-122">Support for disabling package sources</span></span>
<span data-ttu-id="67220-123">Quando vengono configurate più origini dei pacchetti, NuGet avrà un aspetto in ognuno di essi per i pacchetti durante l'installazione di un pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="67220-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="67220-124">Origine pacchetto che non è attivo per qualche motivo possa gravemente rallentare NuGet.</span><span class="sxs-lookup"><span data-stu-id="67220-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="67220-125">Prima di NuGet 1.6, è possibile rimuovere l'origine del pacchetto, ma è necessario tenere presente i dettagli per quando si desidera aggiungerlo di nuovo.</span><span class="sxs-lookup"><span data-stu-id="67220-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="67220-126">NuGet 1.6 consente deselezionando un'origine pacchetto per disabilitarla, ma deve rimanere disponibile.</span><span class="sxs-lookup"><span data-stu-id="67220-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![La disabilitazione di un pacchetto](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="67220-128">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="67220-128">Bug Fixes</span></span>
<span data-ttu-id="67220-129">NuGet 1.6 era un totale di 106 fisso di elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="67220-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="67220-130">95 di questi sono stati classificati sotto forma di bug e 10 di quelli erano le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="67220-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="67220-131">Per un elenco completo di lavoro gli elementi corretti in NuGet 1.6, vista la [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="67220-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
