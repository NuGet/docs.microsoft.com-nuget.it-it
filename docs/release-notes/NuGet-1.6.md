---
title: Note sulla versione 1.6 di NuGet
description: Note sulla versione per NuGet 1.6 inclusi dcr, correzioni di bug, le funzionalità aggiunte e problemi noti.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0345e180893a56302385d27792c4e15ba5d96989
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820599"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="4c59d-103">Note sulla versione 1.6 di NuGet</span><span class="sxs-lookup"><span data-stu-id="4c59d-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="4c59d-104">[Note sulla versione di NuGet 1.5](../release-notes/nuget-1.5.md) | [note sulla versione 1.7 di NuGet](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="4c59d-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="4c59d-105">1.6 NuGet è stato rilasciato il 13 dicembre 2011.</span><span class="sxs-lookup"><span data-stu-id="4c59d-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="4c59d-106">Problema di installazione noti</span><span class="sxs-lookup"><span data-stu-id="4c59d-106">Known Installation Issue</span></span>
<span data-ttu-id="4c59d-107">Se si esegue Visual Studio 2010 SP1, è possibile eseguire in un errore di installazione durante il tentativo di aggiornare NuGet, se è installata una versione precedente.</span><span class="sxs-lookup"><span data-stu-id="4c59d-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="4c59d-108">La soluzione alternativa consiste nel disinstallare semplicemente NuGet e quindi installarlo dalla raccolta di estensioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c59d-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="4c59d-109">Per altre informazioni, vedere [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="4c59d-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="4c59d-110">Nota: Se Visual Studio non consente di disinstallare l'estensione (il pulsante di disinstallazione è disabilitato), quindi probabile che sia necessario riavviare Visual Studio utilizzando "Esegui come amministratore".</span><span class="sxs-lookup"><span data-stu-id="4c59d-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="4c59d-111">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="4c59d-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="4c59d-112">Supporto per il controllo delle versioni semantico e pacchetti della versione provvisoria</span><span class="sxs-lookup"><span data-stu-id="4c59d-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="4c59d-113">1.6 NuGet introduce il supporto per il controllo delle versioni semantico (SemVer).</span><span class="sxs-lookup"><span data-stu-id="4c59d-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="4c59d-114">Per altre informazioni su come viene utilizzato SemVer, leggere la [documentazione di controllo delle versioni](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="4c59d-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="4c59d-115">Uso di NuGet senza l'archiviazione di pacchetti (ripristino del pacchetto)</span><span class="sxs-lookup"><span data-stu-id="4c59d-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="4c59d-116">1.6 NuGet dispone ora di prima classe supporto per il flusso di lavoro in cui NuGet pacchetti non vengono aggiunti al controllo del codice sorgente, ma invece vengono ripristinati in fase di compilazione se mancante.</span><span class="sxs-lookup"><span data-stu-id="4c59d-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="4c59d-117">Per altre informazioni, leggere la [tramite NuGet senza eseguire il commit di pacchetti di controllo del codice sorgente](../consume-packages/packages-and-source-control.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="4c59d-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="4c59d-118">Modelli di elementi che consentono di installare i pacchetti NuGet</span><span class="sxs-lookup"><span data-stu-id="4c59d-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="4c59d-119">Compila il lavoro per supportare pacchetto NuGet preinstallato a modelli di progetto di Visual Studio, 1.6 NuGet aggiunge anche il supporto per i modelli di elemento di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c59d-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="4c59d-120">Modelli di elemento possono essere associate a pacchetti NuGet a cui vengono installati quando il modello nella richiamata.</span><span class="sxs-lookup"><span data-stu-id="4c59d-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="4c59d-121">Per altre informazioni su come modificare un modello di progetto/elemento per installare i pacchetti NuGet, leggere la [pacchetti di modelli di Visual Studio](../visual-studio-extensibility/visual-studio-templates.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="4c59d-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="4c59d-122">Supporto per la disabilitazione dell'origine del pacchetto</span><span class="sxs-lookup"><span data-stu-id="4c59d-122">Support for disabling package sources</span></span>
<span data-ttu-id="4c59d-123">Quando sono configurate più origini del pacchetto, NuGet avrà un aspetto in ognuno di essi per i pacchetti durante l'installazione di un pacchetto e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="4c59d-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="4c59d-124">Origine pacchetto che per qualche motivo può provocare gravi rallentare NuGet non è attivo.</span><span class="sxs-lookup"><span data-stu-id="4c59d-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="4c59d-125">Prima di NuGet 1.6, è possibile rimuovere l'origine del pacchetto, ma è necessario ricordare i dettagli per quando si desidera aggiungerlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="4c59d-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="4c59d-126">1.6 NuGet consente di deselezionare per disabilitarlo, mantenendolo intorno a un'origine del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="4c59d-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![La disabilitazione di un pacchetto](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="4c59d-128">Correzioni di bug</span><span class="sxs-lookup"><span data-stu-id="4c59d-128">Bug Fixes</span></span>
<span data-ttu-id="4c59d-129">1.6 NuGet era un totale di 106 fissati di elementi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4c59d-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="4c59d-130">95 di questi sono stati classificati come bug e 10 di questi sono funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4c59d-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="4c59d-131">Per un elenco completo di lavoro gli elementi corretti in NuGet 1.6,. visualizzazione di [NuGet Issue Tracker per questa versione](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="4c59d-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
